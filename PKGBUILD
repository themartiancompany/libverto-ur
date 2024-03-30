# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Mantas Mikulėnas <grawity@gmail.com>

_pkg=libverto
pkgbase="${_pkg}"
pkgname=(
  "${pkgbase}"
)
pkgver=0.3.2
pkgrel=5
pkgdesc="Main event loop abstraction library"
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'i686'
)
_gh="https://github.com"
_ns="latchset"
_http="${_gh}"
url="${_http}/${_ns}/${_pkg}"
license=(
  'MIT'
)
depends=(
  'glibc'
  'libevent'
)
provides=(
  "${_pkg}.so"
  "${_pkg}-libevent.so"
  "${_pkg}-module-base"
)
conflicts=(
  "krb5<1.19.3-2"
  "${_pkg}-libevent<0.3.2-4"
)
replaces=(
  "${_pkg}-libevent<0.3.2-4"
)
source=(
  "${url}/releases/download/${pkgver}/${_pkg}-${pkgver}.tar.gz"
)
sha256sums=(
  '8d1756fd704f147549f606cd987050fb94b0b1ff621ea6aa4d6bf0b74450468a'
)

build() {
  local \
    _configure_opts=()
  _configure_opts=(
    --prefix="/usr"
    --disable-static
    --with-libevent
    --without-libev
    --without-glib
  )
  cd \
    "${_pkg}-${pkgver}"
  ./configure \
    "${_configure_opts[@]}"
  make
}

check() {
  cd \
    "${pkgname}-${pkgver}"
  make \
    check
}

package_libverto() {
  cd "${_pkg}-${pkgver}"
  make \
    DESTDIR="${pkgdir}" \
    PREFIX="/usr" \
    install
  install \
    -Dm0644 \
    COPYING \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim:set sw=2 sts=-1 et:
