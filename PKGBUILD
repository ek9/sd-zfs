pkgname=mkinitcpio-sd-zfs-encryption
pkgver=1.1.1
pkgrel=1
pkgdesc='Compatibility between systemd and ZFS roots'
license=('MIT')
url='https://github.com/ek9/sd-zfs'
conflicts=('mkinitcpio-sd-zfs')
depends=('mkinitcpio' 'systemd')
source=("https://github.com/ek9/sd-zfs/archive/refs/tags/v${pkgver}.tar.gz")
sha512sums=('b87aafd601abb513cf295227af1c335a1ed677a35db100286ad49e4c1300ee6c449ee6771d5815055d6512952f8786fde400b2fc5ef35d978adbacf8f39d45ac')
arch=('i686' 'x86_64')

build() {
	cd "sd-zfs-${pkgver}"

	make all
}

package() {
	local install bin
	cd "sd-zfs-${pkgver}"

	# mkinitcpio
	for install in sd-zfs{,-shutdown}; do
		install -Dm644 "mkinitcpio-install/${install}" "${pkgdir}/usr/lib/initcpio/install/${install}"
	done

	# binaries
	install -Dm755 zfs-shutdown "${pkgdir}/usr/lib/systemd/system-shutdown/zfs-shutdown"
	for bin in initrd-zfs-generator mount.initrd_zfs; do
		install -Dm755 "${bin}" "${pkgdir}/usr/lib/mkinitcpio-sd-zfs/${bin}"
	done

	# systemd unit
	install -Dm644 units/50-sd-zfs.conf "$pkgdir/usr/lib/tmpfiles.d/50-sd-zfs.conf"
}
