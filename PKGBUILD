# Maintainer: Lucas De Marchi <lucas.de.marchi@gmail.com>
# Contributor: Lucas De Marchi <lucas.de.marchi@gmail.com>

pkgname=connman
pkgver=1.6
pkgrel=1
pkgdesc="Wireless LAN network manager"
url="http://connman.net/"
arch=('i686' 'x86_64')
license=('GPL2')
depends=('dbus-core' 'iptables' 'glib2' 'gnutls')
conflicts=('openresolv')
optdepends=('bluez: Support for Bluetooth devices'
            'wpa_supplicant: For WiFi devices')
makedepends=('bluez' 'wpa_supplicant' 'openconnect' 'openvpn')
options=('!libtool')
source=(connmand-daemon
        http://www.kernel.org/pub/linux/network/${pkgname}/${pkgname}-${pkgver}.tar.bz2
        allow_group_network.diff
       )

build() {
  cd ${srcdir}/${pkgname}-${pkgver}

  patch -Np1 -i ${srcdir}/allow_group_network.diff || return 1

#  for i in ${srcdir}/00*.patch; do
#      patch -Np1 -i $i || return 1
#  done

  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
      --enable-threads \
      --enable-openconnect \
      --enable-openvpn \
      --enable-polkit \
      --enable-client

  make  || return 1
  make DESTDIR=${pkgdir} install || return 1

  install -Dm755 $srcdir/connmand-daemon $pkgdir/etc/rc.d/connmand
}
md5sums=('88ece7cbf1d0d289545ce4f8553fdab8'
         '317fc8603c15fba07478d71c1891e7cb'
         'a8d22ee089fb0ed725130d16ad393047')
