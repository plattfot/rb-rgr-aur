# Maintainer: Fredrik Salomonsson <plattfot@gmail.com>
# Based on hgsreceiver-bin.git AUR
_wacomEnabled=no
pkgname=rgr
pkgver=7.6.1
pkgrel=1
epoch=
pkgdesc="HP Remote Graphics Software, receiver only"
arch=('x86_64')
url="http://www8.hp.com/us/en/campaigns/workstations/remote-graphics-software.html"
license=('custom')
groups=()
depends=('lib32-glu' 'libudev0-shim')
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
source=("RGS_Linux_64_Receiver_v7.6.1_L64929-001.tar.gz")
noextract=()
md5sums=('6b7669e72b01fa0ace61bccf377a57bb')

prepare() {
    bsdtar xf rhel6/receiver/*.rpm
}

package() {
    cd "${srcdir}"

    # install licence
    install -m644 -D rhel6/receiver/LICENSE.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

    chmod 6755 opt/hpremote/rgreceiver/rgsmbiosreader
    chmod 755 etc/opt
    chmod 755 etc/opt/hpremote
    chmod 755 etc/opt/hpremote/*

    # link to libraries included with program
    install -d -m755 etc/ld.so.conf.d
    echo opt/hpremote/rgreceiver/lib64 > etc/ld.so.conf.d/hpremote.conf

    # Install WaCom tablet rules
    if [[ $_wacomEnabled != "no" ]]
    then
        install -d -m755 etc/udev/rules.d
        cp -uf opt/hpremote/rgreceiver/rules/rgs-pen-tablet.rules etc/udev/rules.d/
    fi

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

post-install() {

    /sbin/ldconfig
}
