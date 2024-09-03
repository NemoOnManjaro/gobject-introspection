# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Maintainer: Fabian Bornschein <fabiscafe@archlinux.org>
# Contributor: Jan de Groot <jgc@archlinux.org>

pkgbase=gobject-introspection
pkgname=(
  gobject-introspection
  gobject-introspection-runtime
  libgirepository
)
pkgver=1.81.2
pkgrel=1
pkgdesc="Introspection system for GObject-based libraries"
url="https://wiki.gnome.org/Projects/GObjectIntrospection"
arch=(x86_64)
license=(
  GPL-2.0-or-later
  LGPL-2.0-or-later
)
_glibver=2.82.0
makedepends=(
  "glib2=$_glibver"
  cairo
  git
  glibc
  gtk-doc
  libffi
  libffi
  meson
  python
  python-mako
  python-markdown
  python-setuptools
  python-sphinx
)
source=(
  "git+https://gitlab.gnome.org/GNOME/gobject-introspection.git#tag=$pkgver"
  "git+https://gitlab.gnome.org/GNOME/glib.git?signed#tag=$_glibver"
  "git+https://gitlab.gnome.org/GNOME/gobject-introspection-tests.git"
)
b2sums=('cadb825cb453de7b0e3aa4f2419a7183e2a9d816a53cc9a16cb54b162a882fd38f60f73349ccbba29b95ef267fdb4d0786f078b17778758c3ea4af67538e7c7a'
        '9dee8619918d1bf85d853ddc661c4702046b5361bd3fde105d0b3c550f5dbdbaa6578557107588053bb4e980a21e83b95c2c9e9c7868fb89ca852bc950ac3dba'
        'SKIP')
validpgpkeys=(
  923B7025EE03C1C59F42684CF0942E894B2EAFA0  # Philip Withnall <philip@tecnocode.co.uk>
  D4C501DA48EB797A081750939449C2F50996635F  # Marco Trevisan <marco@trevi.me>
)

prepare() {
  cd $pkgbase

  git submodule init
  git submodule set-url gobject-introspection-tests "${srcdir}/gobject-introspection-tests"
  git -c protocol.file.allow=always -c protocol.allow=never submodule update
}
  
build() {
  local meson_options=(
    -D glib_src_dir="$srcdir/glib"
    -D gtk_doc=true
  )

  arch-meson $pkgbase build "${meson_options[@]}"
  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

_pick() {
  local p="$1" f d; shift
  for f; do
    d="$srcdir/$p/${f#$pkgdir/}"
    mkdir -p "$(dirname "$d")"
    mv "$f" "$d"
    rmdir -p --ignore-fail-on-non-empty "$(dirname "$f")"
  done
}

package_gobject-introspection() {
  depends=(
    "gobject-introspection-runtime=$pkgver-$pkgrel"
    "libgirepository=$pkgver-$pkgrel"
    glib2
    glibc
    libffi
    python
    python-mako
    python-markdown
    python-setuptools
  )

  meson install -C build --destdir "$pkgdir"

  cd "$pkgdir"

  python -m compileall -d /usr/lib/$pkgbase usr/lib/$pkgbase
  python -O -m compileall -d /usr/lib/$pkgbase usr/lib/$pkgbase

  _pick libg usr/include/gobject-introspection-1.0
  _pick libg usr/lib/libgirepository-1.0.so*
  _pick libg usr/lib/pkgconfig/gobject-introspection*-1.0.pc
  _pick libg usr/share/gir-1.0/GIRepository-2.0.gir
  _pick libg usr/share/gtk-doc

  _pick runtime usr/lib/girepository-1.0
}

package_gobject-introspection-runtime() {
  pkgdesc+=" - runtime"
  depends=("libgirepository=$pkgver-$pkgrel")

  mv runtime/* "$pkgdir"
}

package_libgirepository() {
  pkgdesc+=" - runtime library"
  depends=(
    glib2
    glibc
    libffi
    libffi.so
    libg{lib,object,module}-2.0.so
  )
  provides=(libgirepository-1.0.so)

  mv libg/* "$pkgdir"
}

# vim:set sw=2 sts=-1 et:
