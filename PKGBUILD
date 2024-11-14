# Maintainer: Sven-Hendrik Haase <svenstaro@archlinux.org>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Carl George < arch at cgtx dot us >

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=click
pkgname="${_py}-${_pkg}"
pkgver=8.1.7
pkgrel=1
_pkgdesc=(
  "Simple wrapper around optparse"
  "for powerful command line utilities"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  "any"
)
url="https://${_pkg}.palletsprojects.com"
license=(
  "BSD"
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-setuptools"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
)
checkdepends=(
  'python-pytest'
)
_http="https://github.com"
_ns="pallets"
_url="${_http}/${_ns}/${_pkg}"
source=(
  "${_url}/archive/${pkgver}/${pkgname}-${pkgver}.tar.gz"
)
sha512sums=(
  'a1cb115b90193d78f94ec2a6af563b089820517e6e0e4b71ea3d6c68304444d16db3597358c62e1757d9d05449996b7168a220eecde6ab4991367fdb6e74096f'
)

build() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  # https://github.com/pallets/click/issues/2489
  PYTHONPATH="build/lib" \
  pytest \
    -k \
      'not test_bytes_args'
}

package() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm644 \
    "LICENSE.rst" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim:set ts=2 sw=2 et:
