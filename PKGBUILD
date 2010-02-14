# Maintainer: Jan de Groot <jgc@archlinux.org>
pkgname=gobject-introspection
pkgver=0.6.7
pkgrel=1
pkgdesc="Introspection system for GObject-based libraries"
url="http://live.gnome.org/GObjectInstrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('libffi>=3.0.8' 'glib2>=2.23.3' 'python')
options=('!libtool')
source=(http://ftp.gnome.org/pub/gnome/sources/${pkgname}/0.6/${pkgname}-${pkgver}.tar.bz2)
sha256sums=('c97ca4e978b0583999775640e9e9f97b64a5880ad2a6adc3ce903207b616f24a')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --disable-static || return 1
  make || return 1
  make DESTDIR="${pkgdir}" install || return 1
}
