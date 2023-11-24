---
date:
  created: 2023-11-23
  updated: 2023-11-23

tags:
  - Embedded
  - Yocto
  - BitBake
  - Python

comments: true
---
# Install Python Modules in Yocto

## pipoe: A Handy Tool for Embedded World

When developing Python apps in a Yocto project, we may have chances to use some modules that don't come within the default `/meta-openembedded/meta-python` or the version doesn't match our need. Therefore, we have to manually define the `.bb` files for those dependencies and that is a pain in the ass...

Thankfully, there is a tool named [`pipoe`](https://pypi.org/project/pipoe/) working like `pip` but for `oe` (openembedded) that can generate `.bb` files for us (😍).

```shell
pip install pipoe
pipoe --package <target_module> --python <python_version>
```

The generated `.bb` files *should* be ready to go!

## Build by setup.py or Pypi

I believe that most Python developers know that there are many ways of install a module, `pip` with internet, `pip` with `wheel`, source with `setup.py`, yada yada. Although the [community](https://packaging.python.org/en/latest/guides/tool-recommendations/) now is promoting `pyproject.toml` and `pypi` to build, there are still many projects using `setup.py` and `setuptools`. (Please correct me if wrong. I'm not a professional Python developer though.)

Get back to the business. The generated `.bb` files **all** use `setuptools` to build and I've encountered several build errors. To fix these, you can manually change the build method to use `pypi` like me and here's the example.

```apacheconf
# python3-blinker_1.7.0.bb
SUMMARY = "Fast, simple object-to-object and broadcast signaling"
HOMEPAGE = ""
AUTHOR = " <Jason Kirtland <jek@discorporate.us>>"
LICENSE = "MIT"
LIC_FILES_CHKSUM = "file://LICENSE.rst;md5=42cd19c88fc13d1307a4efd64ee90e4e"

SRC_URI = "https://files.pythonhosted.org/packages/a1/13/6df5fc090ff4e5d246baf1f45fe9e5623aa8565757dfa5bd243f6a545f9e/blinker-1.7.0.tar.gz"
SRC_URI[md5sum] = "0306b831281e9918ffb0ac6e3e18b47f"
SRC_URI[sha256sum] = "e6820ff6fa4e4d1d8e2747c2283749c3f547e4fee112b98555cdcdae32996182"

S = "${WORKDIR}/blinker-1.7.0"

RDEPENDS:${PN} = ""

FILES:${PN} += "${libdir}/python3.10/site-packages/blinker"

# change to use pypi
inherit pypi

# manually install to site-packages and copy source there
do_install() {
    install -m 777 -d ${D}${libdir}/python3.10/site-packages/
    cp -r ${S}/src/blinker ${D}${libdir}/python3.10/site-packages/blinker
}
```

## Other Issues

From the above example, you can notice that the source was downloaded from some remote mirror website. Unfortunately, when I tried to install `MarkupSafe`, it seemed to be missing at the remote storage and having some capitailizing problem (*MarkupSafe* and *markupsafe*). So I have to manually download the `.tar.gz` file and install manually.

Here is the exmaple for `MarkupSafe` 2.1.3

```apacheconf
SUMMARY = "Safely add untrusted strings to HTML/XML markup."
HOMEPAGE = "https://palletsprojects.com/p/markupsafe/"
AUTHOR = " <>"
LICENSE = "BSD-3-Clause"
LIC_FILES_CHKSUM = "file://LICENSE.rst;md5=ffeffa59c90c9c4a033c7574f8f3fb75"

# manually download the source and put in `files`
SRC_URI = "file://MarkupSafe-2.1.3.tar.gz"
SRC_URI[md5sum] = "ca33f119bd0551ce15837f58bb180214"
SRC_URI[sha256sum] = "af598ed32d6ae86f1b747b82783958b1a4ab8f617b06fe68795c7f026abbdcad"


S = "${WORKDIR}/MarkupSafe-2.1.3"

RDEPENDS:${PN} = ""

FILES:${PN} += "${libdir}/python3.10/site-packages/markupsafe"

inherit setuptools3

do_install() {
    install -m 777 -d ${D}${libdir}/python3.10/site-packages/
    cp -r ${WORKDIR}/MarkupSafe-2.1.3/src/markupsafe ${D}${libdir}/python3.10/site-packages/markupsafe
}
```