# Maintainer: Jan de Groot <jgc@archlinux.org>
pkgname=gobject-introspection
pkgver=0.6.11
pkgrel=1
pkgdesc="Introspection system for GObject-based libraries"
url="http://live.gnome.org/GObjectInstrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('libffi>=3.0.8' 'glib2>=2.24.1' 'python' 'cairo>=1.8.10')
options=('!libtool')
source=(http://ftp.gnome.org/pub/gnome/sources/${pkgname}/0.6/${pkgname}-${pkgver}.tar.bz2)
sha256sums=('6cbf4b8f5536bb22dd15f89f08673836ce76e3858fb262efd1616899a3d5ca88')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --disable-static || return 1
  make || return 1
  make DESTDIR="${pkgdir}" install || return 1
}
