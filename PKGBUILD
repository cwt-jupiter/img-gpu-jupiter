# Maintainer: Chaiwat Suttipongsakul <cwt@bashell.com>

# IMG GPU PowerVR drivers for SpacemiT K1-x boards.

pkgname=img-gpu-k1x
pkgver=2.0.4
pkgrel=1
pkgdesc="Imagenation GPU DDK for SpacemiT K1-x boards"
url="https://gitee.com/bianbu-linux/img-gpu-powervr"
arch=(riscv64)
license=(BSD-3-Clause)
provides=(opengl-driver vulkan-driver)
optdepends=('libglvnd: to use opengl'
	    'vulkan-icd-loader: to use vulkan'
	    'ocl-icd: to use opencl')
source=("img-gpu-powervr-v${pkgver}.tar.gz::${url}/repository/archive/v${pkgver}.tar.gz"
	'img-gpu-firmware-mkinitcpio.conf'
	'90-img-gpu.rules'
	'IMG.icd')
b2sums=('3dddee9f75fed968c8505ec32e331c5234c009e9e4b1f43a1cc8f2415f827ea139ebac938e7b32b5ce2455214d6de4ec00062b6c23200c4c9a13545334c3f893'
        '016f15dffeef7f1a4a173a74bbdf545640a62aa1c2b95efa49f00e22da26db12cf711d4811f3f7f6d76e489700194d44a02f060000aa617bf235709a9c03d7e9'
        'c84d76962259a47cb056002c4285c7efa9fa51b95cbc7f9fcecade66c05b97250db712ea8006a1b894a226326712e4898f6d6d130826e141ec25b93496bf0569'
        '975dc0305ecd0b6c9f7bb3960c38552d11d85b6b72907e5be0ca6326246b7f75ae67f3f364c91285b52bab05e1da2b2fd146119ec5eff6e6a15e4c38be3fee69')
options=(!strip)

package() {
    cd "${srcdir}/img-gpu-powervr-v${pkgver}/target"

    # Config files
    install -Dm644 etc/powervr.ini "${pkgdir}/etc/powervr.ini"
    install -Dm644 etc/vulkan/icd.d/powervr_icd.json "${pkgdir}/etc/vulkan/icd.d/powervr_icd.json"
    install -Dm644 usr/share/X11/xorg.conf.d/00-noglamoregl.conf "${pkgdir}/usr/share/X11/xorg.conf.d/00-noglamoregl.conf"
    install -Dm644 $srcdir/IMG.icd "${pkgdir}/etc/OpenCL/vendors/IMG.icd"

    # Library files
    for lib in usr/lib/*.so usr/lib/*/*.so; do
        if [ -f $lib ]; then
            install -Dm755 $lib "${pkgdir}/${lib}"
        fi
    done
    # Remove library files that provided by other Arch packages
    rm ${pkgdir}/usr/lib/libGLESv1.so
    rm ${pkgdir}/usr/lib/libGLESv2.so
    rm ${pkgdir}/usr/lib/libvulkan.so
    rm ${pkgdir}/usr/lib/libpvr_mesa_wsi.so

    # Symbolic links
    cp --no-dereference usr/lib/libPVROCL.so.1 "${pkgdir}/usr/lib/libPVROCL.so.1"
    cp --no-dereference usr/lib/libVK_IMG.so.1 "${pkgdir}/usr/lib/libVK_IMG.so.1"

    # Executables
    for bin in usr/local/bin/*; do
        install -Dm755 $bin "${pkgdir}/usr/bin/$(basename $bin)"
    done

    # Shaders
    for shader in usr/local/share/pvr/shaders/*; do
        install -Dm644 $shader "${pkgdir}/usr/share/pvr/shaders/$(basename $shader)"
    done

    # Firmware files
    for firmware in lib/firmware/*; do
        install -Dm644 $firmware "${pkgdir}/usr/${firmware}"
    done
    install -Dm644 $srcdir/img-gpu-firmware-mkinitcpio.conf "${pkgdir}/etc/mkinitcpio.conf.d/${pkgname}.conf"

    # Udev rules
    install -Dm644 $srcdir/90-img-gpu.rules "${pkgdir}/etc/udev/rules.d/90-img-gpu.rules"
}
