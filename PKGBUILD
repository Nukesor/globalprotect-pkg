pkgname=globalprotect-bin
pkgver=6.2.9.1
pkgrel=407
pkgdesc="GlobalProtect VPN client Agent"
arch=('x86_64')
url="https://docs.paloaltonetworks.com/globalprotect/5-2/globalprotect-app-user-guide/globalprotect-app-for-linux/download-and-install-the-globalprotect-app-for-linux"
license=('custom')
groups=()
depends=('wmctrl' 'qt5-webkit')
options=()
source=("local://GlobalProtect_UI_rpm-$pkgver-$pkgrel.rpm")
sha256sums=('58fcd05781c5113a09d46a099b3bd55586d12508f7ba6420f9f295638102df67')

FOLDER="/opt/paloaltonetworks/globalprotect"

prepare() {
    # Replace the "Ubuntu" String with "Arch Linux"
    # The string to replace must be exactly 6 chars long though, which is why we
    # truncate the "Arch Linux" string.
    SEARCH=Ubuntu
    REPLACE=`echo "Arch Linux" | head -c${#SEARCH}`
    TARGET=PanGPS
    sudo sed -i "s/$SEARCH/$REPLACE/g" "${srcdir}$FOLDER/$TARGET"
}

package(){
	# Adapted for Arch Linux from package tarball's install.sh
    cp -r "${srcdir}/opt" "${pkgdir}/opt"
    cp -r "${srcdir}/usr" "${pkgdir}/usr"
    install -d "${srcdir}/usr/bin"
    install -d "${srcdir}/usr/lib"

    # Uncomment this if you want to autostart
    #install -Dm755 "${srcdir}/opt" "${pkgdir}/opt"

    # Service files
	install -Dm644 "${srcdir}${FOLDER}/gpd.service" "${pkgdir}/usr/lib/systemd/system/gpd.service"
	install -Dm644 "${srcdir}${FOLDER}/gpa.service" "${pkgdir}/usr/lib/systemd/user/gpa.service"

    # Symlink globalprotect binary
    ln -s "${FOLDER}/globalprotect" "${pkgdir}/usr/bin/globalprotect"
    # Symlink direct GUI binary
    ln -s "${FOLDER}/PanGPUI" "${pkgdir}/usr/bin/PanGPUI"
}

