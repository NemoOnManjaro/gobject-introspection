# Maintainer: Jan de Groot <jgc@archlinux.org>
pkgname=gobject-introspection
pkgver=0.10.6
pkgrel=1
pkgdesc="Introspection system for GObject-based libraries"
url="http://live.gnome.org/GObjectInstrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('libffi' 'glib2' 'python2')
makedepends=('cairo')
conflicts=('gir-repository')
replaces=('gir-repository')
options=('!libtool')
source=(http://ftp.gnome.org/pub/gnome/sources/${pkgname}/0.10/${pkgname}-${pkgver}.tar.bz2)
sha256sums=('5a72ec875c5d6e9714912bdfed2761903f994e9c5dae841add755b449e014583')

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
