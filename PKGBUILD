# Maintainer: Stefan J. Betz <info at stefan-betz dot net>
# Contributor: p2k <Patrick dot Schneider at uni-ulm dot de>
# Contributor: Jonathan Liu <net147@gmail.com>
# Contributor: Christopher Grebs <cg@webshox.org>
pkgname=rabbitmq
pkgver=2.8.2
pkgrel=1
pkgdesc="Highly reliable and performant enterprise messaging implementation of AMQP written in Erlang/OTP"
arch=('i686' 'x86_64')
url="http://rabbitmq.com"
license=('MPL')
depends=('erlang')
backup=('etc/rabbitmq/rabbitmq.conf' 'etc/rabbitmq/rabbitmq-env.conf')
source=("http://www.rabbitmq.com/releases/${pkgname}-server/v${pkgver}/${pkgname}-server-generic-unix-${pkgver}.tar.gz"
        "rabbitmq-env.conf"
        "rabbitmq-rc.d")
install="${pkgname}.install"
md5sums=('7e9ae4f01341bff61c78bfe7e3ea17be'
         '98da754397bf31c1c172232597ca5943'
         '071d33b65294f60f725cd026400923ab')

package() {
  local libdir="/usr/lib/rabbitmq"
  install -d "${pkgdir}${libdir}"
  cd ${srcdir}
  cp -R ${pkgname}_server-${pkgver}/* "${pkgdir}${libdir}"
  install -d "${pkgdir}/var/log/rabbitmq"
  
  install -d "${pkgdir}/usr/sbin"
  for script in ${pkgdir}${libdir}/sbin/*; do
    ln -s ${script#${pkgdir}} "${pkgdir}/usr/sbin/" 
  done
  install -D rabbitmq-env.conf "${pkgdir}/etc/rabbitmq/rabbitmq-env.conf"
  sed -i 's#^SYS_PREFIX=.*$#SYS_PREFIX="${libdir}"#' "${pkgdir}${libdir}/sbin/rabbitmq-defaults"
  install -D rabbitmq-rc.d "${pkgdir}/etc/rc.d/rabbitmq"
}

# vim:set ts=2 sw=2 et:
