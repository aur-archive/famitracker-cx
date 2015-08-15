# Maintainer: Lara Maia <lara@craft.net.br>

pkgname=famitracker-cx
pkgdesc='NES/Famicom music tracker for Linux'
url='http://code.google.com/p/famitracker-cx/'
pkgrel=3
pkgver=0.4.1a_p4
arch=(x86_64 i686)
license=GPL
depends=('qt4' 'boost-libs')
provices=('famitracker')
conflicts=('famitracker')
makedepends=('cmake' 'boost' 'boost-libs')
optdepends=('jack: For JACK output support'
            'alsa-lib: For ALSA output support')
source=(http://$pkgname.googlecode.com/files/${pkgname}_0.4.1a-p4_src.tar.gz
        $pkgname.desktop
        $pkgname.install)
install=$pkgname.install
sha1sums=('430c021c17958bd2c3b0264742e1e8dd24c6128f'
          'ecb1f9684d34bfd5235566991deff2e1ee523c86'
          'db7bb366ad5e196f4b52f9ca7164914c430b3e43')

build() {
	cd $srcdir
	
	if [ -d "${pkgname}-build" ]; then
		rm -rf ${pkgname}-build/*
	else
		mkdir ${pkgname}-build
	fi
	
	cd ${pkgname}-build
	
	cmake ${srcdir}/${pkgname%%-*}    \
			-DCMAKE_BUILD_TYPE=release \
			-DCMAKE_INSTALL_PREFIX="/usr" \
			-DQT_QMAKE_EXECUTABLE=qmake-qt4
           
   make
}

package() {
	cd "${srcdir}/${pkgname}-build"
	
	make DESTDIR="$pkgdir" install
	
  install -d "$pkgdir"/usr/share/{applications,icons/hicolor/128x128/apps}
  install -m644 "$srcdir"/$pkgname.desktop "$pkgdir"/usr/share/applications/
  install -m644 "$srcdir/${pkgname%%-*}"/src/qt-gui/res/${pkgname%%-*}.png "$pkgdir"/usr/share/icons/hicolor/128x128/apps/
}
