# ImageMagick-how2fix-jessie on docker
This is quick fixation procedures for ImageMagick vulnerability issue on Debian jessie.<BR>
<BR>
https://www.cve.mitre.org/cgi-bin/cvename.cgi?name=2016-3714<BR>
See also.<BR>
https://www.jpcert.or.jp/at/2016/at160021.html<BR>
<BR>
I read two articles bellow, Ref.1 refs PoCs for test, it is useful.<BR>
Ref.2 refs make procedure all worked.<BR>
So, please follow Ref.2 for mainly to make and make install.<BR>
<BR>
Ref.1:<BR>
http://eiua-memo.tumblr.com/post/143934409138/cve-2016-3714imagemagick%E3%81%AE%E3%83%90%E3%83%BC%E3%82%B8%E3%83%A7%E3%83%B3%E3%82%92v701-1%E3%81%AB%E3%82%A2%E3%83%83%E3%83%97%E3%83%87%E3%83%BC%E3%83%88%E3%81%97%E3%81%9F <BR>
Ref.2:<BR>
http://www.linuxfromscratch.org/blfs/view/svn/general/imagemagick.html <BR>
<BR>
#Tested Environment:<BR>
docker-machine version 0.1.0 on OSX Yosemite 10.10.5<BR>
docker image used : https://hub.docker.com/r/sinso/phpfpm-typo3/<BR>
<BR>
Procedures:<BR>
1) apt-get remove ImageMagick<BR>
2) i did follow ref.1 's steps, but error shown bellow on my env.<BR>
convert -list configure<BR>
convert: error while loading shared libraries: http://libMagickCore-7.Q16HDRI.so .0 <BR>
3) switch to ref.2's steps, shown bellow error , but fix to apt-get update then, apt-get intall libperl-dev<BR>
/usr/bin/ld: cannot find -lperl<BR>
collect2: error: ld returned 1 exit status<BR>
so, apt-get install libperl-dev, it fixed.<BR>
4) convert -list configure<BR>
5) convert version<BR>
6) Ref.1 shows how to edit policy.xml and PoCs test, do it.<BR>
shown bellow.<BR>
pwd<BR>
/root/ImageMagick-7.0.1-3/PoCs<BR>
ls<BR>
README.md   http.jpg		msl.jpg  rce1.jpg  read.jpg  test.sh<BR>
delete.jpg  localhost_http.jpg	msl.xml  rce2.jpg  test.png<BR>
./test.sh<BR>
testing read<BR>
SAFE<BR>
<BR>
testing delete<BR>
SAFE<BR>
<BR>
testing http with local port: 48212<BR>
SAFE<BR>
<BR>
testing http with nonce: 8c718117<BR>
SAFE<BR>
<BR>
testing rce1<BR>
SAFE<BR>
<BR>
testing rce2<BR>
SAFE<BR>
<BR>
testing MSL<BR>
SAFE<BR>
<BR>
7) verify on php<BR>
https://stackoverflow.com/questions/4208253/verify-imagemagick-installation<BR>
more d.php<BR>

    <?php
    //This function prints a text array as an html list.
    function alist ($array) {  
      $alist = "<ul>";
      for ($i = 0; $i < sizeof($array); $i++) {
        $alist .= "<li>$array[$i]";
      }
      $alist .= "</ul>";
      return $alist;
    }
    //Try to get ImageMagick "convert" program version number.
    exec("convert -version", $out, $rcode);
    //Print the return code: 0 if OK, nonzero if error.
    echo "Version return code is $rcode <br>";
    //Print the output of "convert -version"
    echo alist($out);
    ?>
<BR># php d.php<BR>
<pre>
Version return code is 1 <br>
<ul>
 <li>Version: ImageMagick 7.0.1-3 Q16 x86_64 2016-05-13 http://www.imagemagick.org<li>Copyright: Copyright (C) 1999-2016 ImageMagick Studio LLC
 <li>License: http://www.imagemagick.org/script/license.php<li>Features: Cipher DPC HDRI OpenMP
 <li>Delegates (built-in): bzlib djvu fontconfig freetype gvc jbig jng jpeg lcms lqr lzma openexr png tiff wmf x xml zlib
</ul>
</pre>
 
