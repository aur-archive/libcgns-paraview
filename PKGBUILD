# Maintainer: Mathias Anselmann <mathias.anselmann@gmail.com>
# Contributor: Thomas Dziedzic < gostrc at gmail >, lainme <lainme993@gmail.com>
# Contributor: Klimov Max <cleemmi@gmail.com>

pkgname=libcgns-paraview
pkgver=3.2.1
pkgrel=1
pkgdesc='General purpose library for the storage and retrieval of computational fluid dynamics analysis data by CGNS standard'
arch=('i686' 'x86_64')
url='http://www.cgns.org'
license=('custom')
conflicts=('libcgns2' 'libcgns')
depends=('tk' 'hdf5' 'libxmu' 'glu')
makedepends=('cmake')
changelog="$pkgname.changelog"
source=("http://downloads.sourceforge.net/project/cgns/cgnslib_${pkgver:0:3}/cgnslib_${pkgver:0:5}.tar.gz")
md5sums=('2d26f88b2058dcd0ee5ce58f483bfccb')

# need to tell cmake when to build 64bit version
if [[ $CARCH == "x86_64" ]]
then
  _64bits=ON
else
  _64_bits=OFF
fi

build() {

  mkdir -p build
  cd build

  cmake \
  -DCGNS_BUILD_SHARED:BOOL=ON \
  -DCMAKE_BUILD_TYPE:STRING="Release" \
  -DCMAKE_INSTALL_PREFIX:PATH=/usr \
  -DCMAKE_VERBOSE_MAKEFILE:BOOL=ON \
  -DCMAKE_SKIP_RPATH:BOOL=ON \
  -DCGNS_BUILD_CGNSTOOLS:BOOL=ON \
  -DCGNS_ENABLE_64BIT:BOOL=${_64bits} \
  -DCGNS_ENABLE_FORTRAN:BOOL=ON \
  -DCGNS_ENABLE_HDF5:BOOL=ON \
  -DCGNS_ENABLE_SCOPING:BOOL=OFF \
  -DCGNS_ENABLE_TESTS:BOOL=ON \
  "../cgnslib_${pkgver:0:5}"

  make
}


check() {
  cd build

  make test
}

package() {
  cd build

  make DESTDIR="${pkgdir}" install

  # install license
  install -Dm644 "${srcdir}/cgnslib_${pkgver:0:5}/license.txt" \
    "${pkgdir}/usr/share/licenses/libcgns-paraview"
}
