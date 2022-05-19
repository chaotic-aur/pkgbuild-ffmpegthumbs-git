# Maintainer: Bartosz Slawianowski <me2.legion at gmail dot com>
pkgname=ffmpegthumbs-git
pkgver=r215.188a562
pkgrel=1
pkgdesc="FFmpeg-based thumbnail creator for video files"
arch=('i686' 'x86_64')
url="https://projects.kde.org/projects/kde/kdemultimedia/ffmpegthumbs"
depends=('ffmpeg' 'kio')
conflicts=('ffmpegthumbs')
provides=('ffmpegthumbs')
makedepends=('extra-cmake-modules' 'git')
source=("git+https://invent.kde.org/multimedia/ffmpegthumbs")
license=('GPL')
md5sums=('SKIP')

pkgver() {
  cd ${pkgname%-git}
  _ver="$(grep -m1 'set(PROJECT_VERSION' CMakeLists.txt | cut -d '"' -f2 | tr - .)"
  echo "${_ver}_r$(git rev-list --count HEAD).g$(git rev-parse --short HEAD)"
}

prepare() {
  mkdir -p build
}

build() {
  cd build
  cmake ../ffmpegthumbs \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DLIB_INSTALL_DIR=lib \
    -DKDE_INSTALL_USE_QT_SYS_PATHS=ON \
    -DBUILD_TESTING=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}" install
}

