# Maintainer: Angel Velasquez <angvp@archlinux.org>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>

pkgname=python2-setuptools
pkgver=44.1.1
pkgrel=2
epoch=2
pkgdesc="Easily download, build, install, upgrade, and uninstall Python packages"
arch=('any')
license=('PSF')
url="https://pypi.org/project/setuptools/"
depends=('python2')
makedepends=('git')
provides=('python2-distribute')
replaces=('python2-distribute')
source=("$pkgname-$pkgver.tar.gz::https://github.com/pypa/setuptools/archive/v$pkgver.tar.gz")
sha512sums=('aabddfbd62b95ce7d8e68d582362361d32b91e65e6d00c393593521a2c1c383552e324ae64974049ae9880072c8741e2393e6482cd07ff7dd30615e91e9e1450')

export SETUPTOOLS_INSTALL_WINDOWS_SPECIFIC_FILES=0

prepare() {
  # Remove post-release tag since we are using stable tags
  sed -e '/tag_build = .post/d' \
      -e '/tag_date = 1/d' \
      -i setuptools-$pkgver/setup.cfg

  cd "$srcdir"/setuptools-$pkgver
  sed -i -e "s|^#\!.*/usr/bin/env python|#!/usr/bin/env python2|" setuptools/command/easy_install.py
}

build() {
  cd setuptools-$pkgver
  python2 bootstrap.py
  python2 setup.py build
}

package() {
  cd setuptools-$pkgver
  python2 setup.py install --prefix=/usr --root="$pkgdir" --optimize=1 --skip-build
  rm "$pkgdir"/usr/bin/easy_install
}
