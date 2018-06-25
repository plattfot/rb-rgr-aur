# Maintainer: Fredrik Salomonsson <plattfot@gmail.com>
# Based on hgsreceiver-bin.git AUR
_wacomEnabled=no
pkgname=rgr
pkgver=7.5.0
pkgrel=2
epoch=
pkgdesc="HP Remote Graphics Software, receiver only"
arch=('x86_64')
url="http://www8.hp.com/us/en/campaigns/workstations/remote-graphics-software.html"
license=('custom')
groups=()
depends=('lib32-glu' 'dmidecode')
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
source=("RGS_Linux_64_Receiver_v7.5_L25793-001.tar.gz")
noextract=()
md5sums=('0d72ec806fe89e0aa4974f825c91dd17')

prepare() {
    bsdtar xf rhel6/receiver/*.rpm
}

package() {
    cd "${srcdir}"

    # install licence
    install -m644 -D rhel6/receiver/LICENSE.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

    # hack needed to register advance features 
    # N.B. rgsmbiosreader does not work under KVM/QEMU/OVMF bios, nor kernel greater than 4.4.44
    # next 4 lines replace rgsmbioreader
    mkdir opt/hpremote/registration
    sudo dmidecode -t 1 | grep UUID | tr A-z a-z | tr -d - | cut -c8-80 > opt/hpremote/registration/H264
    mv opt/hpremote/rgreceiver/rgsmbiosreader opt/hpremote/rgreceiver/rgsmbiosreader.old
    echo '#!/bin/sh' > opt/hpremote/rgreceiver/rgsmbiosreader
    echo 'cat /opt/hpremote/registration/H264' >> opt/hpremote/rgreceiver/rgsmbiosreader

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
