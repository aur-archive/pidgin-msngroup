# $Id$
# Maintainer: Alexander Fehr <pizzapunk gmail com>
# Contributor: Lucien Immink <l.immink@student.fnt.hvu.nl>

pkgname=pidgin-msngroup
pkgver=2.5.4
pkgrel=1
pkgdesc="Multi-protocol instant messaging client, with MSN Group patch."
arch=('i686' 'x86_64')
url="http://pidgin.im/"
license=('GPL')
depends=('startup-notification' 'gtkspell' 'libxss' 'gstreamer0.10'
         'nss' 'libsasl' 'python' 'hicolor-icon-theme')
makedepends=('avahi' 'tk' 'ca-certificates' 'intltool')
optdepends=('avahi: Bonjour protocol support'
            'tk: Tcl/Tk scripting support'
            'ca-certificates: SSL CA certificates')
replaces=('gaim')
provides=('pidgin')
conflicts=('pidgin')
options=('!libtool')
install=pidgin.install
source=(http://downloads.sourceforge.net/pidgin/pidgin-$pkgver.tar.bz2
        msn_group_nickname.patch)
md5sums=('295fe533288c821342b660b6fc83bc11'
         '3d2caea2603752d89510e0cd1693b4aa')

build() {
  cd "$srcdir/pidgin-$pkgver"

  patch -p1 < ../msn_group_nickname.patch
  ./configure --prefix=/usr --sysconfdir=/etc --disable-schemas-install --disable-meanwhile \
    --disable-nm --disable-perl --disable-gnutls --enable-cyrus-sasl --disable-doxygen \
    --with-system-ssl-certs=/etc/ssl/certs || return 1
  make || return 1
  make DESTDIR="$pkgdir" install || return 1

  # Remove GConf schema file
  rm -rf "$pkgdir/etc" || return 1
}
