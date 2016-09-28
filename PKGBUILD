# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgbase=gobject-introspection
pkgname=('gobject-introspection' 'gobject-introspection-runtime')
pkgdesc="Introspection system for GObject-based libraries"
pkgver=1.50.0
pkgrel=1
url="https://live.gnome.org/GObjectIntrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('python' 'python-mako')
makedepends=('cairo' 'git')
options=('!emptydirs')
_commit=cee2a4f215d5edf2e27b9964d3cfcb28a9d4941c  # tags/1.50.0^0
source=("git://git.gnome.org/gobject-introspection#commit=$_commit")
sha256sums=('SKIP')

pkgver() {
  cd $pkgbase
  git describe --tags | sed 's/-/+/g'
}

prepare() {
  cd $pkgbase
  NOCONFIGURE=1 ./autogen.sh
}
  
build() {
  cd $pkgbase
  ./configure --prefix=/usr --disable-static --enable-doctool
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
