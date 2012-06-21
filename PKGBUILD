# Maintainer: Stefan J. Betz <info at stefan-betz dot net>
# Contributor: p2k <Patrick dot Schneider at uni-ulm dot de>
# Contributor: Jonathan Liu <net147@gmail.com>
# Contributor: Christopher Grebs <cg@webshox.org>
# Contributor: slacks42 (https://github.com/slacks42)

pkgname=rabbitmq
pkgver=2.8.3
pkgrel=1
pkgdesc="Highly reliable and performant enterprise messaging implementation of AMQP written in Erlang/OTP"
arch=('i686' 'x86_64')
url="http://rabbitmq.com"
license=('MPL')
depends=('erlang')
backup=('etc/rabbitmq/rabbitmq.conf' 'etc/rabbitmq/rabbitmq-env.conf')
source=("http://www.rabbitmq.com/releases/${pkgname}-server/v${pkgver}/${pkgname}-server-generic-unix-${pkgver}.tar.gz"
        "rabbitmq-env.conf" "rabbitmq-rc.d")
install="${pkgname}.install"
sha1sums=()

package() {
  local libdir="usr/lib/rabbitmq"
  cd ${srcdir}

  install -d "${pkgdir}/${libdir}" "${pkgdir}/var/log/rabbitmq" "${pkgdir}/usr/sbin" "${pkgdir}/var/lib/rabbitmq"

  cp -R ${pkgname}_server-${pkgver}/* "${pkgdir}/${libdir}"
  
  for script in ${pkgdir}/${libdir}/sbin/*; do
    script=$(echo $script | sed -e "s,${pkgdir},,")
    ln -s "${script#${pkgdir}}" "${pkgdir}/usr/sbin/" 
  done

  install -D rabbitmq-env.conf "${pkgdir}/etc/rabbitmq/rabbitmq-env.conf"
  sed -i "s,^SYS_PREFIX=.*$,SYS_PREFIX='/${libdir}'," "${pkgdir}/${libdir}/sbin/rabbitmq-defaults"
  install -D rabbitmq-rc.d "${pkgdir}/etc/rc.d/rabbitmq"
}

# vim:set ts=2 sw=2 et:
sha256sums=('cb8aaaad61e0ea1e8d94b3e83e3af440c59f6c55a88e147adc7af0bf85c0f486'
            '50731fc6958d5672de1d3313a91717b32f5ffd721a1c3c3cf553f88ae2f2c935'
            '4c0379ecda0ef53c621f9710279fe9edcd57914b5635ee439c02383fdd39b727')
