# Maintainer: Felipe Magno de Almeida <felipe.m.almeida__at__gmail.com>

pkgbase=rpm-tizen
pkgname=rpm-tizen
pkgver=20160615
pkgrel=1
pkgdesc="Tizen's librpm project"
arch=('i686' 'x86_64')
license=('GPL')
depends=('python2' 'lua51' 'nss')
makedepends=('python2' 'lua51' 'nss')
source=('git+https://git.tizen.org/cgit/tools/librpm-tizen.git#branch=release-20160615')
sha256sums=('SKIP')
conflicts=('rpm-org')

build() {
  cd $srcdir/librpm-tizen
  export CPPFLAGS=`pkg-config --cflags nss`
  export PYTHON=python2
  ./autogen.sh --exec-prefix=/usr --prefix=/usr --disable-dependency-tracking \
               --libdir=/usr/lib/librpm-tizen \
               --with-lua \
               --without-acl \
               --without-cap \
               --enable-shared \
               --enable-python \
               --with-external-db \
               --build=${CARCH}-tizen-linux \
               PYTHON_MODULENAME=rpm_tizen \
               LUA_PKGCONFIG_NAME=lua51
  make ${MAKEFLAGS}
}

package() {
  cd $srcdir/librpm-tizen
  make DESTDIR=$pkgdir install
  install -m644 packaging/rpm-tizen_macros $pkgdir/usr/lib/librpm-tizen/rpm/tizen_macros
  mv $pkgdir/bin/rpm $pkgdir/usr/bin
  rmdir $pkgdir/bin
  #install -d debian/tmp/usr/lib/librpm-tizen/rpm/tizen
  #install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}
