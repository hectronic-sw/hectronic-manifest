hectronic-manifest
==================

This repository contain repo manifests that selects the version of the Yocto
source code layers to build images for Hectronic products.

The different branches in this repository corresponds to different releases of 
Yocto:

| Yocto version | Codename  | Branch    |
|---------------|-----------|-----------|
| 5.2           | Walnascar | walnascar |
| 6.0           | Wrynose   | wrynose   |

And so on.

Short build instructions for each platform are found below. For further
configuration and tweaking, see the online Yocto manual and the BSP manual 
provided with the product.

Intel x86 based products
------------------------

Initialize repo:
```
$ repo init -u https://github.com/hectronic-se/hectronic-manifest -b wrynose -m repo/intel-x86.xml
```

Sync source code:
```
$ repo sync
```

Configure yocto/bitbake:
```
$ TEMPLATECONF=`pwd`/sources/meta-hectronic-x86/conf/templates/h6089-q7x151 . poky/oe-init-build-env
```

Build image:
```
$ bitbake core-image-minimal
```

NXP i.mx based products
-----------------------

Initialize repo:
```
$ repo init -u https://github.com/hectronic-se/hectronic-manifest -b walnascar -m repo/nxp-imx.xml
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


