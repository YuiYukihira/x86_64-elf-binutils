# Maintainer: Lucy Scarlet <yuiyukihira1@gmail.com>

# cross toolchain build order: binutils, headers, gcc (pass 1), w32api, mingwrt, gcc (pass 2)

_target=x86_64-elf
_sysroot=/usr/lib/${_target}

pkgname=${_target}-binutils
_pkgname=binutils
pkgver=2.37
pkgrel=1
pkgdesc="x86_64 ELF (baremetal) binutils"
arch=('i686' 'x86_64')
url="http://www.gnu.org/software/binutils/"
license=('GPL')
depends=('glibc>=2.10.1' 'zlib')
options=('!libtool' '!distcc' '!ccache')
source=(http://ftp.gnu.org/gnu/${_pkgname}/${_pkgname}-${pkgver}.tar.bz2)
md5sums=('bd4381fc03999059ca48822b48d0ebb9')

build() {
  cd ${srcdir}/${_pkgname}-${pkgver}
  mkdir binutils-build && cd binutils-build

  ../configure --prefix=${_sysroot} --bindir=/usr/bin \
    --with-sysroot=${_sysroot} \
    --build=$CHOST --host=$CHOST --target=${_target} \
    --disable-nls --disable-werror
  make
}

package() {
  cd ${srcdir}/${_pkgname}-${pkgver}/binutils-build
  make DESTDIR=${pkgdir}/ install
}
