# Maintainer: Adam Goldsmith <contact@adamgoldsmith.name>

pkgname=opencamlib-git
pkgver=2019.07.84.ged24fa3
pkgrel=1
pkgdesc="Multi-Purpose CNC Toolpath Library"
arch=('i686' 'x86_64')
url="https://github.com/aewallin/opencamlib"
license=('LGPL')
makedepends=('boost' 'cmake') # 'doxygen' 'texlive'
depends=('python' 'boost')
provides=('opencamlib')
conflicts=('opencamlib')
source=("git+https://github.com/aewallin/opencamlib.git")
md5sums=('SKIP')

pkgver() {
  cd opencamlib
  git describe --tags | sed 's/-/./g'
}

build() {
  cd "$srcdir/opencamlib"
  rm -rf {CMakeLists.txt,build,docs,scripts,Dockerfile,dockerinit.sh,.cproject,.project,dockerinit.sh,.github,.gitignore,COPYING,src/{emscriptenlib,nodejslib,npmpackage,deb,Doxyfile,gcc_version.cmake}}
  rm -rf {src/attic/{cutsim*,ocode,qt_*}}

  if [ ! -d  "$srcdir/opencamlib/build" ]; then
    mkdir -p "$srcdir/opencamlib/build";
  fi
  cd "$srcdir/opencamlib/build"
  cmake ../src \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DBUILD_PY_LIB=ON \
        -DUSE_PY_3=ON \
       -DBUILD_DOC=OFF \
       -DBUILD_EMSCRIPTEN_LIB=OFF \
       -DBUILD_NODEJS_LIB=OFF
  make -j `nproc`
}

package() {
  cd "$srcdir/opencamlib/build"
  make install DESTDIR=$pkgdir
}
