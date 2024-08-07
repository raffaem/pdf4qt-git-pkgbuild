# Maintainer: Raffaele Mancuso <raffaelemancuso532 at gmail dot com>
pkgname=pdf4qt-git
pkgver=1.4.0.0.r3.g2a93ca5
pkgrel=1
pkgdesc="Open source PDF editor"
arch=('x86_64')
url="https://jakubmelka.github.io/"
license=('LGPL-3.0-only')
depends=('openssl'
  'libjpeg-turbo'
  'qt6-speech'
  'qt6-svg'
  'qt6-base'
  'openjpeg2'
  'onetbb'
  'lcms2'
  'freetype2'
  'zlib'
  'glibc'
  'gcc-libs'
  'blend2d-git'
  'hicolor-icon-theme'
)
makedepends=('git'
  'cmake'
  'qt6-declarative'
  'qt6-multimedia'
)
optdepends=(
  'flite: Text-To-Speech using flite synthesizer',
  'libspeechd: Text-To-Speech using speechd synthesizer'
)
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=(
  "$pkgname"::'git+https://github.com/JakubMelka/PDF4QT'
  'CMakeListsMain.patch'
  'CMakeListsLib.patch'
  'FindLCMS2.cmake'
  'FixPluginsDir.patch'
)
sha256sums=(
  'SKIP'
  '0aa0803cff10792a2f025cec558ab4851fcc193d92155ede844b8b71776c85e7'
  'd53ecb1906965453b38e7b0e75495f60ee9da141162f39b02ba18ae6885ab31d'
  'fb438faf87211cf3c21c6fa624cedd2ec6af49b03827e1ad230e0202e939a8ec'
  '857271d65f06efe437c1312bb92c40f96afc808a368d6ddcda89a0f4216c613e'
)

pkgver() {
  cd "$srcdir/$pkgname"
  git describe --tags --long --abbrev=7 | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd "$srcdir/$pkgname"
  patch -p1 -i "$srcdir/CMakeListsMain.patch"
  patch -p1 -i "$srcdir/CMakeListsLib.patch"
  patch -p1 -i "$srcdir/FixPluginsDir.patch"
}

build() {
  cmake -B build \
    -S "$pkgname" \
    -DCMAKE_BUILD_TYPE='Release' \
    -DCMAKE_INSTALL_PREFIX='/' \
    -Wno-dev \
    -DCMAKE_MODULE_PATH="$srcdir" \
    -DPDF4QT_INSTALL_DEPENDENCIES=0 \
    -DPDF4QT_LINUX=1
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
