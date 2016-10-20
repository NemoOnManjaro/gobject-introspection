# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgbase=gobject-introspection
pkgname=('gobject-introspection' 'gobject-introspection-runtime')
pkgdesc="Introspection system for GObject-based libraries"
pkgver=1.50.0+1+gb8d92b0
pkgrel=2
url="https://live.gnome.org/GObjectIntrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('python' 'python-mako')
makedepends=('cairo' 'git' 'gtk-doc')
options=('!emptydirs')
_commit=b8d92b0b36b3907ef066e068e33e9309eb0f8ec5  # master
source=("git://git.gnome.org/gobject-introspection#commit=$_commit"
        0001-giscanner-fix-EOF-check-with-flex-2.6.1.patch)
sha256sums=('SKIP'
            'e1333f2eddf23e4d750aa1c39e5fea8264d0586d1916f11188dbd07d4449d81f')

pkgver() {
  cd $pkgbase
  git describe --tags | sed 's/-/+/g'
}

prepare() {
  cd $pkgbase
  patch -Np1 -i ../0001-giscanner-fix-EOF-check-with-flex-2.6.1.patch
  NOCONFIGURE=1 ./autogen.sh
}
  
build() {
  cd $pkgbase
  ./configure --prefix=/usr --disable-static --enable-doctool --enable-gtk-doc
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
  make
}

package_gobject-introspection-runtime() {
  pkgdesc+=" - runtime files"
  depends=('glib2')
  cd $pkgbase
  make DESTDIR="$pkgdir" install-libLTLIBRARIES install-typelibsDATA
}

package_gobject-introspection() {
  depends+=("gobject-introspection-runtime=$pkgver")

  cd $pkgbase
  make DESTDIR="$pkgdir" install
  make DESTDIR="$pkgdir" uninstall-libLTLIBRARIES uninstall-typelibsDATA
}
