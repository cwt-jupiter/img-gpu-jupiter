# Maintainer: Chaiwat Suttipongsakul <cwt@bashell.com>

# IMG GPU PowerVR drivers for SpacemiT K1-x boards.

pkgname=img-gpu-powervr
pkgver=1.0.15
pkgrel=1
pkgdesc="Imagenation GPU DDK for SpacemiT K1-x boards"
url="${_3rdpart_repo}/tree/JH7110_VisionFive2_devel"
arch=(riscv64)
license=(BSD-3-Clause)
provides=(opengl-driver vulkan-driver)
optdepends=('libglvnd: to use opengl'
	    'vulkan-icd-loader: to use vulkan'
	    'ocl-icd: to use opencl')
source=("img-gpu-powervr-v${pkgver}.tar.gz::https://gitee.com/bianbu-linux/${pkgname}/repository/archive/v${pkgver}.tar.gz"
	'img-gpu-firmware-mkinitcpio.conf'
	'90-img-gpu.rules'
	'IMG.icd')
b2sums=('1bd3ac3bcbceead56573fc2b01c4fdc80f8ba1f366ba7ba37bc988644072d67f861de265c4ef4f7433efd9c27b047d1bab83ef2aaa849e7c30956363551fb607'
        '016f15dffeef7f1a4a173a74bbdf545640a62aa1c2b95efa49f00e22da26db12cf711d4811f3f7f6d76e489700194d44a02f060000aa617bf235709a9c03d7e9'
        'c84d76962259a47cb056002c4285c7efa9fa51b95cbc7f9fcecade66c05b97250db712ea8006a1b894a226326712e4898f6d6d130826e141ec25b93496bf0569'
        '975dc0305ecd0b6c9f7bb3960c38552d11d85b6b72907e5be0ca6326246b7f75ae67f3f364c91285b52bab05e1da2b2fd146119ec5eff6e6a15e4c38be3fee69')
options=(!strip)

package() {
    cd "${srcdir}/${pkgname}-v${pkgver}/target"

    # Config files
    install -Dm644 etc/powervr.ini "${pkgdir}/etc/powervr.ini"
    install -Dm644 etc/vulkan/icd.d/powervr_icd.json "${pkgdir}/etc/vulkan/icd.d/powervr_icd.json"
    install -Dm644 usr/share/X11/xorg.conf.d/00-noglamoregl.conf "${pkgdir}/usr/share/X11/xorg.conf.d/00-noglamoregl.conf"
    install -Dm644 $srcdir/IMG.icd "${pkgdir}/etc/OpenCL/vendors/IMG.icd"

    # Library files
    install -Dm755 usr/lib/libGLESv1_CM_PVR_MESA.so "${pkgdir}/usr/lib/libGLESv1_CM_PVR_MESA.so"
    install -Dm755 usr/lib/libGLESv2_PVR_MESA.so "${pkgdir}/usr/lib/libGLESv2_PVR_MESA.so"
    install -Dm755 usr/lib/libglslcompiler.so "${pkgdir}/usr/lib/libglslcompiler.so"
    install -Dm755 usr/lib/libpvr_dri_support.so "${pkgdir}/usr/lib/libpvr_dri_support.so"
    install -Dm755 usr/lib/libPVROCL.so "${pkgdir}/usr/lib/libPVROCL.so"
    install -Dm755 usr/lib/libPVRScopeServices.so "${pkgdir}/usr/lib/libPVRScopeServices.so"
    install -Dm755 usr/lib/libsrv_um.so "${pkgdir}/usr/lib/libsrv_um.so"
    install -Dm755 usr/lib/libsutu_display.so "${pkgdir}/usr/lib/libsutu_display.so"
    install -Dm755 usr/lib/libufwriter.so "${pkgdir}/usr/lib/libufwriter.so"
    install -Dm755 usr/lib/libusc.so "${pkgdir}/usr/lib/libusc.so"
    install -Dm755 usr/lib/libVK_IMG.so "${pkgdir}/usr/lib/libVK_IMG.so"
    install -Dm755 usr/lib/riscv64-linux-gnu/libpvr_mesa_wsi.so "${pkgdir}/usr/lib/riscv64-linux-gnu/libpvr_mesa_wsi.so"

    # Symbolic links
    cp --no-dereference usr/lib/libPVROCL.so.1 "${pkgdir}/usr/lib/libPVROCL.so.1"
    cp --no-dereference usr/lib/libVK_IMG.so.1 "${pkgdir}/usr/lib/libVK_IMG.so.1"

    # Executables
    install -Dm755 usr/local/bin/eglconfigs "${pkgdir}/usr/bin/eglconfigs"
    install -Dm755 usr/local/bin/egldmabuf "${pkgdir}/usr/bin/egldmabuf"
    install -Dm755 usr/local/bin/eglinfo "${pkgdir}/usr/bin/eglinfo"
    install -Dm755 usr/local/bin/geglinfo "${pkgdir}/usr/bin/geglinfo"
    install -Dm755 usr/local/bin/ggles1test1 "${pkgdir}/usr/bin/ggles1test1"
    install -Dm755 usr/local/bin/ggles2test1 "${pkgdir}/usr/bin/ggles2test1"
    install -Dm755 usr/local/bin/ggles3driimage "${pkgdir}/usr/bin/ggles3driimage"
    install -Dm755 usr/local/bin/ggles3eglimage "${pkgdir}/usr/bin/ggles3eglimage"
    install -Dm755 usr/local/bin/ggles3test1 "${pkgdir}/usr/bin/ggles3test1"
    install -Dm755 usr/local/bin/gles1image_external "${pkgdir}/usr/bin/gles1image_external"
    install -Dm755 usr/local/bin/gles1test1 "${pkgdir}/usr/bin/gles1test1"
    install -Dm755 usr/local/bin/gles2test1 "${pkgdir}/usr/bin/gles2test1"
    install -Dm755 usr/local/bin/gles3image_external "${pkgdir}/usr/bin/gles3image_external"
    install -Dm755 usr/local/bin/gles3_render_to_image "${pkgdir}/usr/bin/gles3_render_to_image"
    install -Dm755 usr/local/bin/gles3test1 "${pkgdir}/usr/bin/gles3test1"
    install -Dm755 usr/local/bin/hwperfbin2jsont "${pkgdir}/usr/bin/hwperfbin2jsont"
    install -Dm755 usr/local/bin/ocl_extended_test "${pkgdir}/usr/bin/ocl_extended_test"
    install -Dm755 usr/local/bin/ocl_unit_test "${pkgdir}/usr/bin/ocl_unit_test"
    install -Dm755 usr/local/bin/pvrdebug "${pkgdir}/usr/bin/pvrdebug"
    install -Dm755 usr/local/bin/pvrhtb2txt "${pkgdir}/usr/bin/pvrhtb2txt"
    install -Dm755 usr/local/bin/pvrhtbd "${pkgdir}/usr/bin/pvrhtbd"
    install -Dm755 usr/local/bin/pvrhwperf "${pkgdir}/usr/bin/pvrhwperf"
    install -Dm755 usr/local/bin/pvrlogdump "${pkgdir}/usr/bin/pvrlogdump"
    install -Dm755 usr/local/bin/pvrlogsplit "${pkgdir}/usr/bin/pvrlogsplit"
    install -Dm755 usr/local/bin/pvr_memory_test "${pkgdir}/usr/bin/pvr_memory_test"
    install -Dm755 usr/local/bin/pvrsrvctl "${pkgdir}/usr/bin/pvrsrvctl"
    install -Dm755 usr/local/bin/pvrtld "${pkgdir}/usr/bin/pvrtld"
    install -Dm755 usr/local/bin/rgx_blit_test "${pkgdir}/usr/bin/rgx_blit_test"
    install -Dm755 usr/local/bin/rgx_compute_test "${pkgdir}/usr/bin/rgx_compute_test"
    install -Dm755 usr/local/bin/rgx_kicksync_test "${pkgdir}/usr/bin/rgx_kicksync_test"
    install -Dm755 usr/local/bin/rgx_triangle_test "${pkgdir}/usr/bin/rgx_triangle_test"
    install -Dm755 usr/local/bin/rgx_twiddling_test "${pkgdir}/usr/bin/rgx_twiddling_test"
    install -Dm755 usr/local/bin/rogue2d_fbctest "${pkgdir}/usr/bin/rogue2d_fbctest"
    install -Dm755 usr/local/bin/rogue2d_unittest "${pkgdir}/usr/bin/rogue2d_unittest"
    install -Dm755 usr/local/bin/tqplayer "${pkgdir}/usr/bin/tqplayer"
    install -Dm755 usr/local/bin/weglinfo "${pkgdir}/usr/bin/weglinfo"
    install -Dm755 usr/local/bin/wgles1image_external "${pkgdir}/usr/bin/wgles1image_external"
    install -Dm755 usr/local/bin/wgles1test1 "${pkgdir}/usr/bin/wgles1test1"
    install -Dm755 usr/local/bin/wgles2test1 "${pkgdir}/usr/bin/wgles2test1"
    install -Dm755 usr/local/bin/wgles3test1 "${pkgdir}/usr/bin/wgles3test1"
    install -Dm755 usr/local/bin/wvkbonjour "${pkgdir}/usr/bin/wvkbonjour"
    install -Dm755 usr/local/bin/wvkcompute "${pkgdir}/usr/bin/wvkcompute"
    install -Dm755 usr/local/bin/wvksalut "${pkgdir}/usr/bin/wvksalut"

    # Shaders
    install -Dm644 usr/local/share/pvr/shaders/gles3_IExt_full_screen_quad_fragshader.txt "${pkgdir}/usr/share/pvr/shaders/gles3_IExt_full_screen_quad_fragshader.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3_IExt_full_screen_quad_fragshader_yuv.txt "${pkgdir}/usr/share/pvr/shaders/gles3_IExt_full_screen_quad_fragshader_yuv.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3_IExt_full_screen_quad_vertshader.txt "${pkgdir}/usr/share/pvr/shaders/gles3_IExt_full_screen_quad_vertshader.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3_RTI_full_screen_quad_fragshader.txt "${pkgdir}/usr/share/pvr/shaders/gles3_RTI_full_screen_quad_fragshader.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3_RTI_full_screen_quad_fragshader_yuv.txt "${pkgdir}/usr/share/pvr/shaders/gles3_RTI_full_screen_quad_fragshader_yuv.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3_RTI_full_screen_quad_vertshader.txt "${pkgdir}/usr/share/pvr/shaders/gles3_RTI_full_screen_quad_vertshader.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3_RTI_plain_triangle_fragshader.txt "${pkgdir}/usr/share/pvr/shaders/gles3_RTI_plain_triangle_fragshader.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3_RTI_plain_triangle_fragshader_yuv.txt "${pkgdir}/usr/share/pvr/shaders/gles3_RTI_plain_triangle_fragshader_yuv.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3_RTI_textured_triangle_fragshader.txt "${pkgdir}/usr/share/pvr/shaders/gles3_RTI_textured_triangle_fragshader.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3_RTI_textured_triangle_fragshader_yuv.txt "${pkgdir}/usr/share/pvr/shaders/gles3_RTI_textured_triangle_fragshader_yuv.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3_RTI_triangle_vertshader.txt "${pkgdir}/usr/share/pvr/shaders/gles3_RTI_triangle_vertshader.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3test1_fragshaderA.txt "${pkgdir}/usr/share/pvr/shaders/gles3test1_fragshaderA.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3test1_fragshaderB.txt "${pkgdir}/usr/share/pvr/shaders/gles3test1_fragshaderB.txt"
    install -Dm644 usr/local/share/pvr/shaders/gles3test1_vertshader.txt "${pkgdir}/usr/share/pvr/shaders/gles3test1_vertshader.txt"
    install -Dm644 usr/local/share/pvr/shaders/glsltest1_fragshaderA.txt "${pkgdir}/usr/share/pvr/shaders/glsltest1_fragshaderA.txt"
    install -Dm644 usr/local/share/pvr/shaders/glsltest1_fragshaderB.txt "${pkgdir}/usr/share/pvr/shaders/glsltest1_fragshaderB.txt"
    install -Dm644 usr/local/share/pvr/shaders/glsltest1_vertshader.txt "${pkgdir}/usr/share/pvr/shaders/glsltest1_vertshader.txt"

    # Firmware files
    install -Dm644 lib/firmware/rgx.fw.36.29.52.182 "${pkgdir}/usr/lib/firmware/rgx.fw.36.29.52.182"
    install -Dm644 lib/firmware/rgx.sh.36.29.52.182 "${pkgdir}/usr/lib/firmware/rgx.sh.36.29.52.182"
    install -Dm644 $srcdir/img-gpu-firmware-mkinitcpio.conf "${pkgdir}/etc/mkinitcpio.conf.d/${pkgname}.conf"

    # Udev rules
    install -Dm644 $srcdir/90-img-gpu.rules "${pkgdir}/etc/udev/rules.d/90-img-gpu.rules"
}
