# Maintainer: Jan de Groot <jgc@archlinux.org>

pkgbase=gobject-introspection
pkgname=(gobject-introspection gobject-introspection-runtime)
pkgver=1.56.0
pkgrel=1
pkgdesc="Introspection system for GObject-based libraries"
url="https://wiki.gnome.org/Projects/GObjectIntrospection"
arch=(x86_64)
license=(LGPL GPL)
depends=(python python-mako)
makedepends=(cairo git gtk-doc)
options=(!emptydirs)
_commit=dc5d8dbedc0f3d16344f1a3648970c9783c08370  # tags/1.56.0^0
source=("git+https://gitlab.gnome.org/GNOME/gobject-introspection.git#commit=$_commit")
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
  ./configure --prefix=/usr --disable-static --enable-doctool --enable-gtk-doc
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
  make
}

package_gobject-introspection-runtime() {
  pkgdesc+=" (runtime library)"
  depends=(glib2)
  cd $pkgbase
  make DESTDIR="$pkgdir" install-libLTLIBRARIES install-typelibsDATA
}

package_gobject-introspection() {
  depends+=("gobject-introspection-runtime=$pkgver-$pkgrel")

  cd $pkgbase
  make DESTDIR="$pkgdir" install
  make DESTDIR="$pkgdir" uninstall-libLTLIBRARIES uninstall-typelibsDATA
}
