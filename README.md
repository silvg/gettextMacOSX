gettextMacOSX
=============

Stop searching for answers! This is all you need to know about installing gettext on Mac OSX 10.9 and above

Okay so you have php 5.5 installed but without gettext, because at the time, you didnt need gettext. Don't go through the trouble of uninstalling and reinstalling php. Continue reading please.

A. Start by downloading the latest gettext source.

1. curl -OL http://ftp.gnu.org/pub/gnu/gettext/gettext-0.19.3.tar.xz
2. tar xzf gettext-0.19.3.tar.gz
3. cd gettext-0.19.3
4. ./configure --prefix=usr/bin
5. make
6. sudo make install

B. Assuming you have php installed, go to your php source. If you can't find your php source (like i couldn't) use
find / -name php

1. cd php-5.5.14/ext/gettext
2. phpize      #if this gives you an error, please see Autoconf, section C
3. ./configure --with-gettext
4. make
5. make test (this tells you a lot of useful information)

C. If there are any issues with phpize, download and install Autoconf

1. curl -OL http://ftpmirror.gnu.org/autoconf/autoconf-latest.tar.gz
2. tar xzf autoconf-latest.tar.gz
3. cd autoconf-*
4. ./configure --prefix=/usr/bin
5. make
6. sudo make install
7. Note: if you go to /usr/bin and you see another bin, move all the autoconf files from /usr/bin/bin to /usr/bin
   sudo mv /usr/bin/bin/autoconf /usr/bin
   sudo mv /usr/bin/bin/autoheader /usr/bin
   sudo mv /usr/bin/bin/autom4te /usr/bin
   sudo mv /usr/bin/bin/autoreconf /usr/bin
   sudo mv /usr/bin/bin/autoscan /usr/bin
   sudo mv /usr/bin/bin/autoupdate /usr/bin
   sudo mv /usr/bin/bin/ifnames /usr/bin
8. Remove the empty bin directory
   rmdir bin
9. Make changes in two files:
   /usr/bin/autoconf: line 505: change /usr/bin/bin/autom4te to /usr/bin/autom4te
   /usr/bin/autoheader: find /usr/bin/bin/autom4te and change to /usr/bin/autom4te
10. Go back to section B and phpize again...

D. Copy .so file to YOUR php installation (you may have a different no-debug file)

1. sudo cp modules/gettext.so /usr/lib/php/extensions/no-debug-non-zts-20121212/

E. Update Mavericks/Yosemite's php.ini file to enable gettext

1. sudo vi /etc/php.ini
2. Add this line under extensions: extension=/usr/lib/php/extensions/no-debug-non-zts-20121212/gettext.so

F. Restart Apache

1. sudo apachectl restart

