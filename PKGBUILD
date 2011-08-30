# Maintainer: Jan de Groot <jgc@archlinux.org>
pkgname=gobject-introspection
pkgver=1.29.17
pkgrel=1
pkgdesc="Introspection system for GObject-based libraries"
url="http://live.gnome.org/GObjectInstrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('glib2' 'python2')
makedepends=('cairo')
options=('!libtool')
source=(http://ftp.gnome.org/pub/gnome/sources/${pkgname}/1.29/${pkgname}-${pkgver}.tar.xz)
sha256sums=('ce1cc5a9a992151f91d56ec1a0d424e3fe019e58b74fef02a133d91ed8dcebfe')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  PYTHON=/usr/bin/python2 ./configure --prefix=/usr --disable-static
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install

  sed -i '1s|#!/usr/bin/env python$|&2|' \
    "${pkgdir}"/usr/lib/gobject-introspection/giscanner/*.py
}
