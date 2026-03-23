pkgname=mkinitcpio-sd-zfs-encryption
pkgver=1.1.0
pkgrel=1
pkgdesc='Compatibility between systemd and ZFS roots'
license=('MIT')
url='https://github.com/ek9/sd-zfs'
conflicts=('mkinitcpio-sd-zfs')
depends=('mkinitcpio' 'systemd')
source=("https://github.com/ek9/sd-zfs/archive/refs/tags/v${pkgver}.tar.gz")
sha512sums=('9925efc9de020486af8de611837218eb491afee9689eeb0ee56b75d8e1185cd1fbdb294390265ea1fbc53bfee13ec0a011798827a1b2a9fe89b9d70fac75e0f0')
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
