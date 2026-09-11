hectronic-manifest
==================

This is the manifest branch that support Yocut Wrynose builds for Hectronic
products.

Short build instructions for each platform are found below. For further
configuration and tweaking, see the online Yocto manual and the BSP manual 
provided with the product.

Intel x86 based products
------------------------

Initialize repo:
```
mkdir -p x86-yocto && cd $_
repo init -u https://github.com/hectronic-sw/hectronic-manifest -b wrynose -m repo/intel-x86.xml
repo sync
```

Configure yocto/bitbake:
```
TEMPLATECONF=`pwd`/sources/meta-hectronic-x86/conf/templates/h1190 . sources/openembedded-core/oe-init-build-env build-h1190
```

Add local changes (to speedup rebuild during development)
 - conf/local.conf
    - INHERIT += "rm_work"
 - conf/site.conf
    - DL_DIR ?= "${BSPDIR}/../downloads/"
    - SSTATE_DIR ?= "${BSPDIR}/../sstate-cache/"

Build image:
```
bitbake core-image-minimal
```


NXP i.MX based products
-----------------------

Initialize repo:
```
mkdir -p nxp-yocto && cd $_
repo init -u https://github.com/hectronic-sw/hectronic-manifest -b wrynose -m repo/nxp-imx.xml
repo sync
```

Configure yocto/bitbake:
```
MACHINE=h6095-smx331 DISTRO=fsl-imx-xwayland . imx-setup-release.sh -b build-h6095
echo 'BBLAYERS += "${BSPDIR}/sources/meta-hectronic-imx"' >> conf/bblayers.conf
```

Add local changes (to speedup rebuild during development)
 - conf/local.conf
    - INHERIT += "rm_work"
 - conf/site.conf
    - DL_DIR ?= "${BSPDIR}/../downloads/"
    - SSTATE_DIR ?= "${BSPDIR}/../sstate-cache/"

Build image:
```
bitbake core-image-minimal
```

