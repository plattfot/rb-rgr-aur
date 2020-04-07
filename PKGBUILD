# Maintainer: Fredrik Salomonsson <plattfot@gmail.com>
# Based on hgsreceiver-bin.git AUR
_wacomEnabled=no
pkgname=rb-rgr
pkgver=20.0.0.23427
pkgrel=2
epoch=
pkgdesc="HP ZCentral Remote Boost Software (Receiver Only)"
arch=('x86_64')
url="https://www8.hp.com/us/en/workstations/zcentral-remote-boost.html"
license=('custom')
groups=()
depends=()
makedepends=()
checkdepends=()
optdepends=()
provides=()
conflicts=('rgr')
replaces=()
backup=()
options=()
install=
changelog=
source=("ZCentral_RB_2020.0_Linux_Receiver_M08155-001.tar.gz")
noextract=()
md5sums=('db8fe90fe324c6f5c7e6f8454c2d37c1')

prepare() {
    bsdtar xf rhel7-8/receiver/*.rpm
}

package() {
    cd "${srcdir}"

    # install licence
    install -m644 -D rhel7-8/receiver/LICENSE.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

    chmod 755 etc/opt
    chmod 755 etc/opt/hpremote
    chmod 755 etc/opt/hpremote/*

    # copy the directories
    cp -rpf ./opt/ $pkgdir
    cp -rpf ./etc/ $pkgdir
    cp -rpf ./usr/ $pkgdir
    cp -rpf ./source/ $pkgdir

    # install executable in /usr/bin
    install -dm755 $pkgdir/usr/bin
    echo -e "#!/bin/bash\n/opt/hpremote/rgreceiver/rgreceiver.sh" > $pkgdir/usr/bin/rgr
    chmod 755 $pkgdir/usr/bin/rgr
}
