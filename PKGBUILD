# Maintainer: Jan de Groot <jgc@archlinux.org>
pkgname=gobject-introspection
pkgver=0.9.5
pkgrel=1
pkgdesc="Introspection system for GObject-based libraries"
url="http://live.gnome.org/GObjectInstrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('libffi>=3.0.9' 'glib2>=2.25.15' 'python2')
makedepends=('cairo')
options=('!libtool')
source=(http://ftp.gnome.org/pub/gnome/sources/${pkgname}/0.9/${pkgname}-${pkgver}.tar.bz2)
sha256sums=('93ea75860b468f1439a3735b3b132707afbb785867c00b1a5d7841697c4d5964')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --disable-static
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
}
