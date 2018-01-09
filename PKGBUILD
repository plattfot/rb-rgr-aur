# Maintainer: Fredrik Salomonsson <plattfot@gmail.com>
pkgname=rgr
pkgver=7.4.0.13800
pkgrel=1
epoch=
pkgdesc="HP Remote Graphics Software, receiver only"
arch=('x86_64')
url="http://www8.hp.com/us/en/campaigns/workstations/remote-graphics-software.html"
license=('custom')
groups=()
depends=('libpng12' 'libudev0')
makedepends=()
checkdepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=("RGS_Linux_64_Receiver_v7.4_L01911-001.tar.gz")
noextract=()
md5sums=('SKIP') #generate with 'makepkg -g'

prepare() {
    mkdir -p ${srcdir}/pkg
    bsdtar -C ${srcdir}/pkg -xf ${srcdir}/ubuntu/receiver/rgreceiver_linux_64-${pkgver}-1.${arch}.rpm
    chmod 755 -R ${srcdir}/pkg
}

package() {
    # install src
    cp -r $srcdir/pkg/* $pkgdir/
    chmod 755 -R $pkgdir/*
    install -dm755 $pkgdir/usr/bin
    # install executable in /usr/bin
    echo -e "#!/bin/bash\n/opt/hpremote/rgreceiver/rgreceiver.sh" > $pkgdir/usr/bin/rgr
    chmod 755 $pkgdir/usr/bin/rgr
    # install license
    install -Dm644 $srcdir/ubuntu/receiver/LICENSE.txt \
            $pkgdir/usr/share/licenses/$pkgname/license.txt
}
