# GCC for Raspberry Pi

This repo store the binaries of GCC compiled for RPI.
I compiled it for Raspberry Pi 2 B.
I may compile it for other RPI if requested ... and if I have one.

## How to install
Download the file:
`wget https://github.com/inares/gcc-for-raspberry/raw/gcc-8.2.0/gcc-8.2.0-rpi2b-binaries.tar.bz2`

Extract the file:
#### `tar -C /usr/local/ -xjf gcc-8.2.0-rpi2b-binaries.tar.bz2`
This will extract the files in /usr/local/gcc-8.2.0

-----

## How to compile GCC on RPI ([v8.2.0](https://gcc.gnu.org/))

This is based on the work of [Solarian](https://solarianprogrammer.com/2017/12/07/raspberry-pi-raspbian-compiling-gcc/).

```
cd ~
wget https://mirror.ibcp.fr/pub/gnu/gcc/gcc-8.2.0/gcc-8.2.0.tar.gz
tar xf gcc-8.2.0.tar.gz
cd gcc-8.2.0
contrib/download_prerequisites
cd ~
mkdir -p gcc-8.2.0_build/tmp && cd gcc-8.2.0_build
export TMPDIR=$HOME/gcc-8.2.0_build/tmp
../gcc-8.2.0/configure -v --enable-languages=c,c++ --prefix=/usr/local/gcc-8.2.0 --program-suffix=-8.2.0 --with-arch=armv7-a --with-fpu=neon-vfpv4 --with-float=hard --build=arm-linux-gnueabihf --host=arm-linux-gnueabihf --target=arm-linux-gnueabihf --enable-shared --enable-linker-build-id --without-included-gettext --enable-threads=posix --enable-nls --with-sysroot=/ --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --with-default-libstdcxx-abi=new --enable-gnu-unique-object --disable-libitm --disable-libquadmath --enable-plugin --with-system-zlib --disable-browser-plugin --with-target-system-zlib --enable-objc-gc=auto --enable-multiarch
make -j 4
sudo make install-strip
cd /usr/local/
sudo chown pi:pi -R gcc-8.2.0/
tar -cjf $HOME/gcc-8.2.0-rpi2b+.tar.bz2 gcc-8.2.0/
```

