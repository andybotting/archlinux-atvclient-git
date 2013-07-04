pkgname=atvclient-git
pkgver=20130325
pkgrel=1
pkgdesc="Background application implementing the functionality of the AppleTV OS HID driver"
arch=('i686' 'x86_64')
url="http://wiki.github.com/Evinyatar/atvclient/"
license=('GPL2')
depends=('libusb-compat')
makedepends=('git')
source=(atvclient.service
        atvclient.conf)
sha1sums=('fd9cf44a834c5f688d00b91f763700fad799aac8'
          '19f073c1dc4b96766148b59311ce0eb214eaa520')
changelog=$pkgname.changelog
install=$pkgname.install
_gitroot='git://github.com/Evinyatar/atvclient.git'
_gitname='atvclient'

build() {

    cd ${srcdir}

    msg "Connecting to GIT server...."

    if [ -d ${srcdir}/${_gitname} ] ; then
        cd ${_gitname} && git pull origin
        msg "The local files are updated."
    else
        git clone ${_gitroot}
        cd ${_gitname}
    fi

    autoreconf
    ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var --sbindir=/usr/bin
    make

}

package() {

    cd ${srcdir}/${_gitname}
    make install DESTDIR=${pkgdir}
    
    install -d -m 755 ${pkgdir}/etc/conf.d/
    install -d -m 755 ${pkgdir}/usr/lib/systemd/system/
    install -m 755 ${srcdir}/${source[0]} ${pkgdir}/usr/lib/systemd/system/atvclient.service
    install -m 644 ${srcdir}/${source[1]} ${pkgdir}/etc/conf.d/atvclient

    install -d -m 755 ${pkgdir}/usr/share/doc/${pkgname}/
    install -m 644 {AUTHORS,NEWS,README,COPYING,ChangeLog} ${pkgdir}/usr/share/doc/${pkgname}/

}

