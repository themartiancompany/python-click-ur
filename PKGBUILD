# Maintainer: Sven-Hendrik Haase <svenstaro@archlinux.org>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Carl George < arch at cgtx dot us >

pkgname=python-click
_realname=click
pkgver=8.1.5
pkgrel=1
pkgdesc="Simple wrapper around optparse for powerful command line utilities"
arch=("any")
url='https://click.palletsprojects.com/'
license=("BSD")
depends=("python")
makedepends=('python-setuptools' 'python-build' 'python-installer' 'python-wheel')
checkdepends=('python-pytest')
source=("https://github.com/pallets/click/archive/${pkgver}/$pkgname-$pkgver.tar.gz")
sha512sums=('55171a5f16643305c6d9b038ff6c72bdfbbdeb4c39e7dbc04618fceba2345b2a4d69925d3490ea5a974be4101c8b1f4c0dd3b247d9b050506bb92a6a7d6334cb')

build() {
  cd "${srcdir}/${_realname}-${pkgver}"
  python -m build --wheel --no-isolation
}

check() {
  cd "${srcdir}/${_realname}-${pkgver}"
  # https://github.com/pallets/click/issues/2489
  PYTHONPATH="build/lib" pytest -k 'not test_bytes_args'
}

package() {
  cd "${srcdir}/${_realname}-${pkgver}"
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -Dm 644 "LICENSE.rst" -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim:set ts=2 sw=2 et:
