# Maintainer: Fredrik Salomonsson <plattfot@gmail.com>
# Based on hgsreceiver-bin.git AUR
_wacomEnabled=no
pkgname=rb-rgr
pkgver=20.1.0.26348
pkgrel=3
epoch=
pkgdesc="HP ZCentral Remote Boost Software (Receiver Only)"
arch=('x86_64')
url="https://www8.hp.com/us/en/workstations/zcentral-remote-boost.html"
license=('custom')
groups=()
depends=('lib32-glu')
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
source=("ZCentral_RB_2020.1.0_Linux_Receiver_M39127-001.tar.gz")
noextract=()
sha256sums=('f409373bc29dd10c38bc0f9340ed17f017b77d19d903985abf9f524665e1e1c9')

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

    # Remove QT_QPA_PLATFORM from the environment as that will
    # segfault the program if it is set to wayland.
    sed -Ei 's|Exec=(.*)|Exec=env -u QT_QPA_PLATFORM \1|' usr/share/applications/hp-rgreceiver.desktop
    # copy the directories
    cp -rpf ./opt/ $pkgdir
    cp -rpf ./etc/ $pkgdir
    cp -rpf ./usr/ $pkgdir
    cp -rpf ./source/ $pkgdir
}
