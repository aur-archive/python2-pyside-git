# Maintainer: Michael Schubert <mschu.dev at gmail>
# Contributor: Matthias Maennich <arch@maennich.net>
# Contributor: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>

pkgname=python2-pyside-git
pkgver=20130308
pkgrel=1
pkgdesc="Provides LGPL Qt bindings for Python and related tools for binding generation."
arch=('i686' 'x86_64')
license=('LGPL')
url="http://www.pyside.org"
depends=('shiboken-git' 'python2' 'qt4>=4.8' 'phonon' 'mesa')
makedepends=('cmake' 'automoc4' 'git')
provides=('python2-pyside')
conflicts=('python2-pyside')

_gitroot="git://github.com/PySide/PySide.git"
_gitname="PySide"

build(){
    cd "$srcdir"

    msg "Connecting to GIT server...."
    if [ -d "${srcdir}/${_gitname}" ] ; then
        cd ${_gitname} && git pull --rebase
    else
        git clone ${_gitroot}
        cd ${_gitname}
    fi

    mkdir build && cd build
    cmake .. -DQT_QMAKE_EXECUTABLE=qmake-qt4 -DCMAKE_INSTALL_PREFIX=/usr \
        -DQT_PHONON_INCLUDE_DIR=/usr/include/phonon \
        -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTS=OFF
    VERBOSE=1 make
}

package(){
    cd "$srcdir/$_gitname/build"
    make DESTDIR="$pkgdir" install
}

