# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

#Maintainer gee
#Based of primecoin-qt by Daniel Spies

pkgname=dogecoin-qt-git
_gitname=dogecoin
_binname=dogecoin
pkgver=v1.7.0.r0.g20c2a7e
pkgrel=2
pkgdesc="Cryptocurrency"
arch=('x86_64' 'i686')
url="http://dogecoin.com/"
license=('MIT')
provides=('dogecoin-qt')
depends=('qt4' 'miniupnpc' 'boost-libs')
makedepends=('boost' 'gcc' 'make' 'git')
source=('git+https://github.com/dogecoin/dogecoin.git'
        'dogecoin.desktop')
install=dogecoin.install

sha256sums=(SKIP
            '679d16a093c3f8d92d9ad0f0cd4af8888e2ceae7ba507caabd1ba0d5e56f5d76')

## files & commands for building
_qmake=qmake-qt4

pkgver() {
	cd "$srcdir/${_gitname}"
	git describe --long --tags | sed -E 's/([^-]*-g)/r\1/;s/-/./g'
}
    

build() {
	cd ${_gitname}
	
	#${_qmake} ${_binname}-qt.pro
	
	./autogen.sh
	
	./configure --with-incompatible-bdb
		
	make 
	#${MAKEFLAGS} || make ${MAKEFLAGS}
}

package() {
	install -Dm644 ${_binname}.desktop ${pkgdir}/usr/share/applications/${_binname}.desktop

	cd ${_gitname}
	install -Dm755 src/qt/${_binname}-qt "$pkgdir"/usr/bin/${_binname}-qt
	install -Dm755 src/${_binname}-cli "$pkgdir"/usr/bin/${_binname}-cli
	install -Dm755 src/${_binname}d "$pkgdir"/usr/bin/${_binname}d
	install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
	install -Dm644 src/qt/res/icons/bitcoin.png "$pkgdir"/usr/share/pixmaps/${_binname}.png
}
