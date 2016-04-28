# $Id$
# Maintainer: BlackIkeEagle <ike DOT devolder AT gmail DOT com>
# Contributor: Kevin Piche <kevin@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# vim: set ft=sh:

pkgname=fwbuilder
pkgver=5.1.0.3599
pkgrel=7
pkgdesc="Object-oriented GUI and set of compilers for various firewall platforms"
url="http://www.fwbuilder.org/"
arch=('i686' 'x86_64')
license=('GPL')
depends=('libxslt' 'net-snmp' 'qt4' 'desktop-file-utils' 'hicolor-icon-theme' 'shared-mime-info')
conflicts=('libfwbuilder')
source=("http://sourceforge.net/projects/fwbuilder/files/Current_Packages/${pkgver%.*}/fwbuilder-${pkgver}.tar.gz"
		'fwbuilder.xml'
		'fwbuilder-gcc47.patch')
sha256sums=('452514a1ec0be1416bfca93603e6c89deb91d1a3a19671c64b5a8868a3743daf'
			'f8eacaa9895b17af3a1c148064b5ad8381b83f7983acb14687faef488ac8fede'
			'd7c602d5b99c6e40403c0b02e34abf15de83802257ca5ce80ad53d486b692f27')

build() {
  cd "${srcdir}/fwbuilder-${pkgver}"
  patch -p1 -i "$srcdir/fwbuilder-gcc47.patch"
  export CXXFLAGS="$CXXFLAGS -fno-var-tracking-assignments"
  ./autogen.sh
  ./configure --prefix=/usr
  make
}

package() {
  cd "${srcdir}/fwbuilder-${pkgver}"
  make INSTALL_ROOT="${pkgdir}" install
  echo "MimeType=text/x-xml-fwbuilder;" >> "$pkgdir/usr/share/applications/${pkgname}.desktop"
  install -Dm644 "$srcdir/fwbuilder.xml" "$pkgdir/usr/share/mime/packages/fwbuilder.xml"
}
