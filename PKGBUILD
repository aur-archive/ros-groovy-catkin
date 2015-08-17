pkgdesc="ROS - Low-level build system macros and infrastructure."
url='http://www.ros.org/'

pkgname='ros-groovy-catkin'
pkgver='0.5.77'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(
  cmake
  python2-nose
  python2-empy
  gtest
  python2-catkin_pkg)

source=()

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/catkin ]; then
    cd ${srcdir}/catkin
    git fetch origin --tags
    git reset --hard release/groovy/catkin/${pkgver}-0
  else
    git clone -b release/groovy/catkin/${pkgver}-0 git://github.com/ros-gbp/catkin-release.git ${srcdir}/catkin
  fi
  cd ${srcdir}
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/catkin
  cmake ${srcdir}/catkin -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
md5sums=('2504a2d050595b55023fa699530dfb99')
