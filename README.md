# ImageMagick-how2fix-jessie-
This is quick fixation procedures for ImageMagick vulnerability issue on Debian jessie.<BR>
I read two articles bellow, Ref.1 refs PoCs for test, it is useful.<BR>
Ref.2 refs make procedure all worked.<BR>
So, please follow Ref.2 for mainly to make and make install.<BR>
<BR>
Ref.1:<BR>
http://eiua-memo.tumblr.com/post/143934409138/cve-2016-3714imagemagick%E3%81%AE%E3%83%90%E3%83%BC%E3%82%B8%E3%83%A7%E3%83%B3%E3%82%92v701-1%E3%81%AB%E3%82%A2%E3%83%83%E3%83%97%E3%83%87%E3%83%BC%E3%83%88%E3%81%97%E3%81%9F <BR>
Ref.2:<BR>
http://www.linuxfromscratch.org/blfs/view/svn/general/imagemagick.html <BR>
<BR>
Tested Environment:<BR>
docker-machine version 0.1.0 on OSX Yosemite 10.10.5<BR>
https://hub.docker.com/r/sinso/phpfpm-typo3/<BR>
apt-get remove ImageMagick<BR>
<BR>
Procedures:<BR>
1) i did follow ref.1 's steps, but error shown bellow on my env.<BR>
# convert -list configure<BR>
convert: error while loading shared libraries: http://libMagickCore-7.Q16HDRI.so .0 <BR>
2) switch to ref.2's steps, shown bellow error , but fix to apt-get update then, apt-get intall libperl-dev<BR>
/usr/bin/ld: cannot find -lperl<BR>
collect2: error: ld returned 1 exit status<BR>
so, apt-get install libperl-dev, it fixed.<BR>
3) convert -list configure<BR>
4) convert version<BR>
5) Ref.1 shows how to edit policy.xml and PoCs test, do it.<BR>
