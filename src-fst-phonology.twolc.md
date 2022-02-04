=================================== !
# The Hungarian morphophonological/twolc rules file 
=================================== !

This file documents the [phonology.twolc file](http://github.com/giellalt/lang-hun/blob/main/src/fst/phonology.twolc) 

## Alphabets and sets

*  a b c d e f g h i j k l m n o p q r s t u v w x y z  
   á é ó ú í ö ü ő ű  
   æ ø å à è ò ù ì ä ë ï â ê ô û î ã ý þ ñ ð ß ç  

*  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z  
  Á É Ó Ú Í Ö Ü Ő Ű  
*  Æ Ø Å À È Ò Ù Ì Ä Ë Ï Â Ê Ô Û Î Ã Ý Þ Ñ Ð ß Ç  

TRIGGERS
* %{back%}:0  
* %{front%}:0  
* %^Ö2:0		 h%^Ö2z
* %^V2:0		 %^V2al 
* %^Hist:0          historic documents
* %^Pen:0		 penultimate position
* %^RmVow:0	 remove vowel
* %^V2VV:0	 lengthen vowel
* %^VV2V:0	 shorten vowel

Archiphones
* %{ae%}:a %{ae%}:e  
* %{aeáé%}:a %{aeáé%}:e %{aeáé%}:á %{aeáé%}:é  
* %{áé%}:á %{áé%}:é  
* %{eoö%}:e %{eoö%}:o %{eoö%}:ö  
* %{óő%}:ó %{óő%}:ő  
* %{uü%}:u %{uü%}:ü  
*  %>  

Sets

*  Vow = a e i o u á é ó ú í ő ű ö ü  
        A E I O U Á É Ó Ú Í Ő Ű Ö Ü  
        æ ø å à è ò ù ì ä ë ö ü ï â ê ô û î ã ý ;  
*  VowAndY = Vow y Y ;  

*  Cns = b c d f g h j k l m n p q r s t v w x z ð þ   
        B C D F G H J K L M N P Q R S T V W X Z Ð Þ ;  

## Rules 

Rule: **Stem-final vowel lengthening** 
béke+N+Sg+PxSg3
* *béke%^V2VV%>je*
* *béké0%>je*

Rule: **Penultimate Stem vowel shortening** 
madár+N+Pl+Nom
* *madár%^Pen%^VV2V%>ak*
* *madar00%>ak*

Rule: **Penultimate and stem-final vowel removal** 
forradalom+N+Pl+Nom
* *forradalom%{back%}%^Pen%^RmVow%>%{ae%}k*
* *forradal0m000%>ak*

falu+N+Pl+Nom
* *falu%^RmVow%>vak*
* *fal00%>vak*

Rule: **Assimilation to stem-final consonant** 

Rule: **Assimilation to stem-final consonant followed by y** 

Rule: **Assimilation to stem-final zs cs ** 

Rule: **Assimilation to stem-final sz** 

Rule: **v from V2** 


fül+N+Sg+Nom+PxPl2
* *fül%{front%}%>%{ae%}t%{eoö%}k*
* *fül0%>etek*

Rule: **%{eoö%} to o** 


Rule: **low vowel variation a e back** 
* *ház%{back%}%>b%{ae%}n*
* *ház0%>ban*

* ★*ház%{back%}%>b%{ae%}n* (is not standard language)
* ★*ház0%>ben* (is not standard language)

Rule: **low vowel variation a e front short** 



Rule: **low vowel variation a e á é back short** 

Rule: **low vowel variation a e á é back long** 

Rule: **low vowel variation a e á é front short** 

Rule: **low vowel variation a e á é front long** 


Rule: **long mid vowel variation ó ő back ** 

Rule: **long mid vowel variation ó ő front ** 

Rule: **long high vowel variation u ü back ** 

Rule: **long high vowel variation u ü front ** 

* * *
<small>This (part of) documentation was generated from [../src/fst/phonology.twolc](http://github.com/giellalt/lang-hun/blob/main/../src/fst/phonology.twolc)</small>