# Maintainer: Kevin Sarendranath k.sarendranath@gmail.com
# Based on brother-mfc-j4510dw package from AUR

_model="j470dw"
pkgname="brother-mfc-$_model"
pkgver="3.0.0"
pkgrel=1
_revision=1
pkgdesc="LPR and CUPS driver for the Brother MFC-J470DW. Based on the brother-mfc-j4510dw package, all credit goes to raudi"
url="http://welcome.solutions.brother.com/bsc/public_s/id/linux/en/index.html"
arch=('i686' 'x86_64')
license='unknown'
install="brother-mfc-${_model}.install"
depends=('tcsh' 'deb2targz' 'perl' 'a2ps')
source=("http://www.brother.com/pub/bsc/linux/dlf/mfc${_model}lpr-${pkgver}-${_revision}.i386.deb"
    "http://www.brother.com/pub/bsc/linux/dlf/mfc${_model}cupswrapper-${pkgver}-${_revision}.i386.deb")
md5sums=('20b923565536e94732a946e91ac3719f'
         '5bf2fed1702e94a06e3b9332d9c29bf1')


build() {
    deb2targz *.deb >/dev/null || return 1
    rm -f *.deb || return 1
    cd $srcdir || return 1
    [ -d "mfc${_model}" ] || (mkdir mfc${_model} || return 1)
    for i in *.tar.gz;do tar xfz $i -C mfc${_model};done || return 1
    cd mfc${_model} || return 1
    cd opt/brother/Printers/mfc${_model} || return 1
    perl -i -pe 's#/etc/init.d#/etc/rc.d#g' ./cupswrapper/cupswrappermfc${_model} || return 1
    perl -i -pe 's#printcap\.local#printcap#g' $srcdir/mfc${_model}/opt/brother/Printers/mfc${_model}/inf/setupPrintcapij || return 1
    cp -rf $srcdir/mfc${_model}/usr/ $pkgdir/ || return 1
    cp -rf $srcdir/mfc${_model}/opt/ $pkgdir/ || return 1
}
