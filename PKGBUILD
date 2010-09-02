# Maintainer: Jan de Groot <jgc@archlinux.org>
pkgname=gobject-introspection
pkgver=0.6.14
pkgrel=2
pkgdesc="Introspection system for GObject-based libraries"
url="http://live.gnome.org/GObjectInstrospection"
arch=('x86_64' 'i686')
license=('LGPL' 'GPL')
depends=('libffi>=3.0.8' 'glib2>=2.24.1' 'python2' 'cairo>=1.8.10')
options=('!libtool')
source=(http://ftp.gnome.org/pub/gnome/sources/${pkgname}/0.6/${pkgname}-${pkgver}.tar.bz2
        python2.7-compat.patch)
sha256sums=('c4713bcbcebb06861738a8f630ab05289666e631f42f7abbf2e836978db7eba6'
            '7b3864502e011cd3fa31db9460bcda35e3e20f93962b8e546c3257232e14750e')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  # Python2.7 compatibility:
  # https://bugzilla.gnome.org/show_bug.cgi?id=618562
  patch -p1 -i "$srcdir"/python2.7-compat.patch
  ./configure --prefix=/usr --disable-static || return 1
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
}
