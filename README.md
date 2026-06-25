hectronic-manifest
==================

This is the manifest branch that support Yocut Walnascar builds for Hectronic
products.

Short build instructions for each platform are found below. For further
configuration and tweaking, see the online Yocto manual and the BSP manual 
provided with the product.

NXP i.mx based products
-----------------------

Initialize repo:
```
=======
$ repo init -u https://github.com/hectronic-sw/hectronic-manifest -b walnascar -m repo/nxp-imx.xml
```

Sync source code:
```
$ repo sync
```

Configure yocto/bitbake:
```
$ MACHINE=h6095-smx331 DISTRO=fsl-imx-xwayland . imx-setup-release.sh -b build-h6095
$ echo 'BBLAYERS += "${BSPDIR}/sources/meta-hectronic-imx"' >> conf/bblayers.conf
```

Build image:
```
$ bitbake core-image-minimal
```

