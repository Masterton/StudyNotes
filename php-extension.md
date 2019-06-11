# PHP扩展编译安装

* php扩展下载地址 [下载地址](http://pecl.php.net/package-stats.php)

```
# 下载
wget -c http://pecl.php.net/get/igbinary-3.0.1.tgz

# 解压
root@zheng:~# tar -zxvf igbinary-3.0.1.tgz
package.xml
igbinary-3.0.1/tests/igbinary_001.phpt
igbinary-3.0.1/tests/igbinary_002.phpt
igbinary-3.0.1/tests/igbinary_003.phpt
igbinary-3.0.1/tests/igbinary_004.phpt
igbinary-3.0.1/tests/igbinary_005.phpt
igbinary-3.0.1/tests/igbinary_006.phpt
igbinary-3.0.1/tests/igbinary_007.phpt
igbinary-3.0.1/tests/igbinary_008.phpt
igbinary-3.0.1/tests/igbinary_009.phpt
igbinary-3.0.1/tests/igbinary_009b.phpt
igbinary-3.0.1/tests/igbinary_010.phpt
igbinary-3.0.1/tests/igbinary_012.phpt
igbinary-3.0.1/tests/igbinary_013.phpt
igbinary-3.0.1/tests/igbinary_014.phpt
igbinary-3.0.1/tests/igbinary_015.phpt
igbinary-3.0.1/tests/igbinary_015b.phpt
igbinary-3.0.1/tests/igbinary_015c.phpt
igbinary-3.0.1/tests/igbinary_016.phpt
igbinary-3.0.1/tests/igbinary_017.phpt
igbinary-3.0.1/tests/igbinary_018.phpt
igbinary-3.0.1/tests/igbinary_019.phpt
igbinary-3.0.1/tests/igbinary_020.phpt
igbinary-3.0.1/tests/igbinary_021.phpt
igbinary-3.0.1/tests/igbinary_022.phpt
igbinary-3.0.1/tests/igbinary_023.phpt
igbinary-3.0.1/tests/igbinary_024.phpt
igbinary-3.0.1/tests/igbinary_025.phpt
igbinary-3.0.1/tests/igbinary_025b.phpt
igbinary-3.0.1/tests/igbinary_026.phpt
igbinary-3.0.1/tests/igbinary_026b.phpt
igbinary-3.0.1/tests/igbinary_027.phpt
igbinary-3.0.1/tests/igbinary_028.phpt
igbinary-3.0.1/tests/igbinary_029.phpt
igbinary-3.0.1/tests/igbinary_030_php72.phpt
igbinary-3.0.1/tests/igbinary_030_php7.phpt
igbinary-3.0.1/tests/igbinary_031.phpt
igbinary-3.0.1/tests/igbinary_032.phpt
igbinary-3.0.1/tests/igbinary_033.phpt
igbinary-3.0.1/tests/igbinary_034.phpt
igbinary-3.0.1/tests/igbinary_040.phpt
igbinary-3.0.1/tests/igbinary_041.phpt
igbinary-3.0.1/tests/igbinary_043.phpt
igbinary-3.0.1/tests/igbinary_044.phpt
igbinary-3.0.1/tests/igbinary_045b.phpt
igbinary-3.0.1/tests/igbinary_045c.phpt
igbinary-3.0.1/tests/igbinary_046.phpt
igbinary-3.0.1/tests/igbinary_046b.phpt
igbinary-3.0.1/tests/igbinary_046c.phpt
igbinary-3.0.1/tests/igbinary_046d.phpt
igbinary-3.0.1/tests/igbinary_047.phpt
igbinary-3.0.1/tests/igbinary_048.phpt
igbinary-3.0.1/tests/igbinary_048b.phpt
igbinary-3.0.1/tests/igbinary_049.phpt
igbinary-3.0.1/tests/igbinary_049b.phpt
igbinary-3.0.1/tests/igbinary_050.phpt
igbinary-3.0.1/tests/igbinary_051.phpt
igbinary-3.0.1/tests/igbinary_052.phpt
igbinary-3.0.1/tests/igbinary_053.phpt
igbinary-3.0.1/tests/igbinary_054.phpt
igbinary-3.0.1/tests/igbinary_055.phpt
igbinary-3.0.1/tests/igbinary_057.phpt
igbinary-3.0.1/tests/igbinary_058.phpt
igbinary-3.0.1/tests/igbinary_058b.phpt
igbinary-3.0.1/tests/igbinary_059.phpt
igbinary-3.0.1/tests/igbinary_060.phpt
igbinary-3.0.1/tests/igbinary_061.phpt
igbinary-3.0.1/tests/igbinary_062.phpt
igbinary-3.0.1/tests/igbinary_063_php72.phpt
igbinary-3.0.1/tests/igbinary_063_php7.phpt
igbinary-3.0.1/tests/igbinary_064.phpt
igbinary-3.0.1/tests/igbinary_065.phpt
igbinary-3.0.1/tests/igbinary_066.phpt
igbinary-3.0.1/tests/igbinary_067.phpt
igbinary-3.0.1/tests/igbinary_068.phpt
igbinary-3.0.1/tests/igbinary_069.phpt
igbinary-3.0.1/tests/igbinary_bug54662.phpt
igbinary-3.0.1/tests/igbinary_bug72134.phpt
igbinary-3.0.1/tests/igbinary_unserialize_v1_compatible.phpt
igbinary-3.0.1/config.m4
igbinary-3.0.1/config.w32
igbinary-3.0.1/igbinary.h
igbinary-3.0.1/php_igbinary.h
igbinary-3.0.1/src/php7/hash.h
igbinary-3.0.1/src/php7/hash_ptr.h
igbinary-3.0.1/src/php7/hash_si.c
igbinary-3.0.1/src/php7/hash_si_ptr.c
igbinary-3.0.1/src/php7/igbinary.c
igbinary-3.0.1/src/php7/igbinary.h
igbinary-3.0.1/src/php7/igbinary_macros.h
igbinary-3.0.1/src/php7/php_igbinary.h
igbinary-3.0.1/src/php7/ig_win32.h
igbinary-3.0.1/igbinary.php
igbinary-3.0.1/igbinary.php.ini
igbinary-3.0.1/tags.sh
igbinary-3.0.1/igbinary.spec
igbinary-3.0.1/COPYING
igbinary-3.0.1/CREDITS
igbinary-3.0.1/README.md
igbinary-3.0.1/NEWS
```

* 1、在扩展解压包目录执行

```
root@zheng:~/igbinary-3.0.1# ll
total 72
drwxr-xr-x  4 root  root  4096 Jun 11 10:45 ./
drwxr-xr-x 10 root  root  4096 Jun 11 10:45 ../
-rw-rw-r--  1 zheng zheng 2876 Mar 21 07:51 config.m4
-rw-rw-r--  1 zheng zheng 1767 Mar 21 07:51 config.w32
-rw-r--r--  1 zheng zheng 1551 Mar 21 07:51 COPYING
-rw-rw-r--  1 zheng zheng  549 Mar 21 07:51 CREDITS
-rw-rw-r--  1 zheng zheng  235 Mar 21 07:51 igbinary.h
-rw-rw-r--  1 zheng zheng 3544 Mar 21 07:51 igbinary.php
-rw-r--r--  1 zheng zheng  136 Mar 21 07:51 igbinary.php.ini
-rw-r--r--  1 zheng zheng 1606 Mar 21 07:51 igbinary.spec
-rw-rw-r--  1 zheng zheng 4484 Mar 21 07:51 NEWS
-rw-rw-r--  1 zheng zheng  762 Mar 21 07:51 php_igbinary.h
-rw-rw-r--  1 zheng zheng 5863 Mar 21 07:51 README.md
drwxr-xr-x  3 root  root  4096 Jun 11 10:45 src/
-rwxr-xr-x  1 zheng zheng  211 Mar 21 07:51 tags.sh*
drwxr-xr-x  2 root  root  4096 Jun 11 10:45 tests/
root@zheng:~/igbinary-3.0.1# phpize
Configuring for:
PHP Api Version:         20151012
Zend Module Api No:      20151012
Zend Extension Api No:   320151012
root@zheng:~/igbinary-3.0.1# ll
total 1496
drwxr-xr-x  6 root  root    4096 Jun 11 10:47 ./
drwxr-xr-x 10 root  root    4096 Jun 11 10:45 ../
-rw-r--r--  1 root  root   82685 Jun 11 10:47 acinclude.m4
-rw-r--r--  1 root  root  414799 Jun 11 10:47 aclocal.m4
drwxr-xr-x  2 root  root    4096 Jun 11 10:47 autom4te.cache/
drwxr-xr-x  2 root  root    4096 Jun 11 10:47 build/
-rwxr-xr-x  1 root  root   43499 Jun 11 10:47 config.guess*
-rw-r--r--  1 root  root    2046 Jun 11 10:47 config.h.in
-rw-rw-r--  1 zheng zheng   2876 Mar 21 07:51 config.m4
-rwxr-xr-x  1 root  root   36144 Jun 11 10:47 config.sub*
-rwxr-xr-x  1 root  root  428873 Jun 11 10:47 configure*
-rw-r--r--  1 root  root    4698 Jun 11 10:47 configure.in
-rw-rw-r--  1 zheng zheng   1767 Mar 21 07:51 config.w32
-rw-r--r--  1 zheng zheng   1551 Mar 21 07:51 COPYING
-rw-rw-r--  1 zheng zheng    549 Mar 21 07:51 CREDITS
-rw-rw-r--  1 zheng zheng    235 Mar 21 07:51 igbinary.h
-rw-rw-r--  1 zheng zheng   3544 Mar 21 07:51 igbinary.php
-rw-r--r--  1 zheng zheng    136 Mar 21 07:51 igbinary.php.ini
-rw-r--r--  1 zheng zheng   1606 Mar 21 07:51 igbinary.spec
-rw-r--r--  1 root  root       0 Jun 11 10:47 install-sh
-rw-r--r--  1 root  root  324404 Jun 11 10:47 ltmain.sh
-rw-r--r--  1 root  root    7135 Jun 11 10:47 Makefile.global
-rw-r--r--  1 root  root       0 Jun 11 10:47 missing
-rw-r--r--  1 root  root       0 Jun 11 10:47 mkinstalldirs
-rw-rw-r--  1 zheng zheng   4484 Mar 21 07:51 NEWS
-rw-rw-r--  1 zheng zheng    762 Mar 21 07:51 php_igbinary.h
-rw-rw-r--  1 zheng zheng   5863 Mar 21 07:51 README.md
-rw-r--r--  1 root  root   83249 Jun 11 10:47 run-tests.php
drwxr-xr-x  3 root  root    4096 Jun 11 10:45 src/
-rwxr-xr-x  1 zheng zheng    211 Mar 21 07:51 tags.sh*
drwxr-xr-x  2 root  root    4096 Jun 11 10:45 tests/
root@zheng:~/igbinary-3.0.1#
```

* 2、执行 ./configure --with-php-config=/usr/bin/php-config

```
root@zheng:~/igbinary-3.0.1# whereis php-config
php-config: /usr/bin/php-config /usr/bin/php-config7.0 /usr/share/man/man1/php-config.1.gz
root@zheng:~/igbinary-3.0.1# ./configure --with-php-config=/usr/bin/php-config
checking for grep that handles long lines and -e... /bin/grep
checking for egrep... /bin/grep -E
checking for a sed that does not truncate output... /bin/sed
checking for cc... cc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether cc accepts -g... yes
checking for cc option to accept ISO C89... none needed
checking how to run the C preprocessor... cc -E
checking for icc... no
checking for suncc... no
checking whether cc understands -c and -o together... yes
checking for system library directory... lib
checking if compiler supports -R... no
checking if compiler supports -Wl,-rpath,... yes
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking target system type... x86_64-pc-linux-gnu
checking for PHP prefix... /usr
checking for PHP includes... -I/usr/include/php/20151012 -I/usr/include/php/20151012/main -I/usr/include/php/20151012/TSRM -I/usr/include/php/20151012/Zend -I/usr/include/php/20151012/ext -I/usr/include/php/20151012/ext/date/lib
checking for PHP extension directory... /usr/lib/php/20151012
checking for PHP installed headers prefix... /usr/include/php/20151012
checking if debug is enabled... no
checking if zts is enabled... no
checking for re2c... no
configure: WARNING: You will need re2c 0.13.4 or later if you want to regenerate PHP parsers.
checking for gawk... no
checking for nawk... nawk
checking if nawk is broken... no
checking whether to enable igbinary support... yes, shared
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for unistd.h... yes
checking stdbool.h usability... yes
checking stdbool.h presence... yes
checking for stdbool.h... yes
checking stddef.h usability... yes
checking stddef.h presence... yes
checking for stddef.h... yes
checking for stdint.h... (cached) yes
checking PHP version... PHP 7
checking for APCu includes... not found
checking size of long... 8
checking compiler type... gcc
checking how to print strings... printf
checking for a sed that does not truncate output... (cached) /bin/sed
checking for fgrep... /bin/grep -F
checking for ld used by cc... /usr/bin/ld
checking if the linker (/usr/bin/ld) is GNU ld... yes
checking for BSD- or MS-compatible name lister (nm)... /usr/bin/nm -B
checking the name lister (/usr/bin/nm -B) interface... BSD nm
checking whether ln -s works... yes
checking the maximum length of command line arguments... 1572864
checking how to convert x86_64-pc-linux-gnu file names to x86_64-pc-linux-gnu format... func_convert_file_noop
checking how to convert x86_64-pc-linux-gnu file names to toolchain format... func_convert_file_noop
checking for /usr/bin/ld option to reload object files... -r
checking for objdump... objdump
checking how to recognize dependent libraries... pass_all
checking for dlltool... no
checking how to associate runtime and link libraries... printf %s\n
checking for ar... ar
checking for archiver @FILE support... @
checking for strip... strip
checking for ranlib... ranlib
checking for gawk... (cached) nawk
checking command to parse /usr/bin/nm -B output from cc object... ok
checking for sysroot... no
checking for a working dd... /bin/dd
checking how to truncate binary pipes... /bin/dd bs=4096 count=1
checking for mt... mt
checking if mt is a manifest tool... no
checking for dlfcn.h... yes
checking for objdir... .libs
checking if cc supports -fno-rtti -fno-exceptions... no
checking for cc option to produce PIC... -fPIC -DPIC
checking if cc PIC flag -fPIC -DPIC works... yes
checking if cc static flag -static works... yes
checking if cc supports -c -o file.o... yes
checking if cc supports -c -o file.o... (cached) yes
checking whether the cc linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking whether -lc should be explicitly linked in... no
checking dynamic linker characteristics... GNU/Linux ld.so
checking how to hardcode library paths into programs... immediate
checking whether stripping libraries is possible... yes
checking if libtool supports shared libraries... yes
checking whether to build shared libraries... yes
checking whether to build static libraries... no
configure: creating ./config.status
config.status: creating config.h
config.status: executing libtool commands
root@zheng:~/igbinary-3.0.1# 
```

* 3、编译 make&&make install （安装完成后在php安装目录下的扩展目录就会有相应的.so扩展文件。）

```
root@zheng:~/igbinary-3.0.1# make&&make insall
/bin/bash /home/zheng/igbinary-3.0.1/libtool --mode=compile cc -g -O2 -O2 -Wall -Wpointer-arith -Wcast-align -Wwrite-strings -Wswitch -finline-limit=10000 --param large-function-growth=10000 --param inline-unit-growth=10000 -I. -I/home/zheng/igbinary-3.0.1 -DPHP_ATOM_INC -I/home/zheng/igbinary-3.0.1/include -I/home/zheng/igbinary-3.0.1/main -I/home/zheng/igbinary-3.0.1 -I/usr/include/php/20151012 -I/usr/include/php/20151012/main -I/usr/include/php/20151012/TSRM -I/usr/include/php/20151012/Zend -I/usr/include/php/20151012/ext -I/usr/include/php/20151012/ext/date/lib  -DHAVE_CONFIG_H  -g -O2   -c /home/zheng/igbinary-3.0.1/src/php7/igbinary.c -o src/php7/igbinary.lo 
libtool: compile:  cc -g -O2 -O2 -Wall -Wpointer-arith -Wcast-align -Wwrite-strings -Wswitch -finline-limit=10000 --param large-function-growth=10000 --param inline-unit-growth=10000 -I. -I/home/zheng/igbinary-3.0.1 -DPHP_ATOM_INC -I/home/zheng/igbinary-3.0.1/include -I/home/zheng/igbinary-3.0.1/main -I/home/zheng/igbinary-3.0.1 -I/usr/include/php/20151012 -I/usr/include/php/20151012/main -I/usr/include/php/20151012/TSRM -I/usr/include/php/20151012/Zend -I/usr/include/php/20151012/ext -I/usr/include/php/20151012/ext/date/lib -DHAVE_CONFIG_H -g -O2 -c /home/zheng/igbinary-3.0.1/src/php7/igbinary.c  -fPIC -DPIC -o src/php7/.libs/igbinary.o
/bin/bash /home/zheng/igbinary-3.0.1/libtool --mode=compile cc -g -O2 -O2 -Wall -Wpointer-arith -Wcast-align -Wwrite-strings -Wswitch -finline-limit=10000 --param large-function-growth=10000 --param inline-unit-growth=10000 -I. -I/home/zheng/igbinary-3.0.1 -DPHP_ATOM_INC -I/home/zheng/igbinary-3.0.1/include -I/home/zheng/igbinary-3.0.1/main -I/home/zheng/igbinary-3.0.1 -I/usr/include/php/20151012 -I/usr/include/php/20151012/main -I/usr/include/php/20151012/TSRM -I/usr/include/php/20151012/Zend -I/usr/include/php/20151012/ext -I/usr/include/php/20151012/ext/date/lib  -DHAVE_CONFIG_H  -g -O2   -c /home/zheng/igbinary-3.0.1/src/php7/hash_si.c -o src/php7/hash_si.lo 
libtool: compile:  cc -g -O2 -O2 -Wall -Wpointer-arith -Wcast-align -Wwrite-strings -Wswitch -finline-limit=10000 --param large-function-growth=10000 --param inline-unit-growth=10000 -I. -I/home/zheng/igbinary-3.0.1 -DPHP_ATOM_INC -I/home/zheng/igbinary-3.0.1/include -I/home/zheng/igbinary-3.0.1/main -I/home/zheng/igbinary-3.0.1 -I/usr/include/php/20151012 -I/usr/include/php/20151012/main -I/usr/include/php/20151012/TSRM -I/usr/include/php/20151012/Zend -I/usr/include/php/20151012/ext -I/usr/include/php/20151012/ext/date/lib -DHAVE_CONFIG_H -g -O2 -c /home/zheng/igbinary-3.0.1/src/php7/hash_si.c  -fPIC -DPIC -o src/php7/.libs/hash_si.o
/bin/bash /home/zheng/igbinary-3.0.1/libtool --mode=compile cc -g -O2 -O2 -Wall -Wpointer-arith -Wcast-align -Wwrite-strings -Wswitch -finline-limit=10000 --param large-function-growth=10000 --param inline-unit-growth=10000 -I. -I/home/zheng/igbinary-3.0.1 -DPHP_ATOM_INC -I/home/zheng/igbinary-3.0.1/include -I/home/zheng/igbinary-3.0.1/main -I/home/zheng/igbinary-3.0.1 -I/usr/include/php/20151012 -I/usr/include/php/20151012/main -I/usr/include/php/20151012/TSRM -I/usr/include/php/20151012/Zend -I/usr/include/php/20151012/ext -I/usr/include/php/20151012/ext/date/lib  -DHAVE_CONFIG_H  -g -O2   -c /home/zheng/igbinary-3.0.1/src/php7/hash_si_ptr.c -o src/php7/hash_si_ptr.lo 
libtool: compile:  cc -g -O2 -O2 -Wall -Wpointer-arith -Wcast-align -Wwrite-strings -Wswitch -finline-limit=10000 --param large-function-growth=10000 --param inline-unit-growth=10000 -I. -I/home/zheng/igbinary-3.0.1 -DPHP_ATOM_INC -I/home/zheng/igbinary-3.0.1/include -I/home/zheng/igbinary-3.0.1/main -I/home/zheng/igbinary-3.0.1 -I/usr/include/php/20151012 -I/usr/include/php/20151012/main -I/usr/include/php/20151012/TSRM -I/usr/include/php/20151012/Zend -I/usr/include/php/20151012/ext -I/usr/include/php/20151012/ext/date/lib -DHAVE_CONFIG_H -g -O2 -c /home/zheng/igbinary-3.0.1/src/php7/hash_si_ptr.c  -fPIC -DPIC -o src/php7/.libs/hash_si_ptr.o
/bin/bash /home/zheng/igbinary-3.0.1/libtool --mode=link cc -DPHP_ATOM_INC -I/home/zheng/igbinary-3.0.1/include -I/home/zheng/igbinary-3.0.1/main -I/home/zheng/igbinary-3.0.1 -I/usr/include/php/20151012 -I/usr/include/php/20151012/main -I/usr/include/php/20151012/TSRM -I/usr/include/php/20151012/Zend -I/usr/include/php/20151012/ext -I/usr/include/php/20151012/ext/date/lib  -DHAVE_CONFIG_H  -g -O2   -o igbinary.la -export-dynamic -avoid-version -prefer-pic -module -rpath /home/zheng/igbinary-3.0.1/modules  src/php7/igbinary.lo src/php7/hash_si.lo src/php7/hash_si_ptr.lo 
libtool: link: cc -shared  -fPIC -DPIC  src/php7/.libs/igbinary.o src/php7/.libs/hash_si.o src/php7/.libs/hash_si_ptr.o    -g -O2   -Wl,-soname -Wl,igbinary.so -o .libs/igbinary.so
libtool: link: ( cd ".libs" && rm -f "igbinary.la" && ln -s "../igbinary.la" "igbinary.la" )
/bin/bash /home/zheng/igbinary-3.0.1/libtool --mode=install cp ./igbinary.la /home/zheng/igbinary-3.0.1/modules
libtool: install: cp ./.libs/igbinary.so /home/zheng/igbinary-3.0.1/modules/igbinary.so
libtool: install: cp ./.libs/igbinary.lai /home/zheng/igbinary-3.0.1/modules/igbinary.la
libtool: finish: PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/sbin" ldconfig -n /home/zheng/igbinary-3.0.1/modules
----------------------------------------------------------------------
Libraries have been installed in:
   /home/zheng/igbinary-3.0.1/modules

If you ever happen to want to link against installed libraries
in a given directory, LIBDIR, you must either use libtool, and
specify the full pathname of the library, or use the '-LLIBDIR'
flag during linking and do at least one of the following:
   - add LIBDIR to the 'LD_LIBRARY_PATH' environment variable
     during execution
   - add LIBDIR to the 'LD_RUN_PATH' environment variable
     during linking
   - use the '-Wl,-rpath -Wl,LIBDIR' linker flag
   - have your system administrator add LIBDIR to '/etc/ld.so.conf'

See any operating system documentation about shared libraries for
more information, such as the ld(1) and ld.so(8) manual pages.
----------------------------------------------------------------------

Build complete.
Don't forget to run 'make test'.

Installing shared extensions:     /usr/lib/php/20151012/
Installing header files:          /usr/include/php/20151012/
root@zheng:~/igbinary-3.0.1# 
```

* 4、配置支持php 修改php.ini 在最后一行添加以下内容  extension= 扩展文件名.so

```
[igbinary]
extension=igbinary.so
```

* 5、重启服务

```
root@zheng:~/igbinary-3.0.1# systemctl restart php7.0-fpm.service
```