---
date:
  created: 2023-11-23
  updated: 2023-11-28

description: >
  Tutorial for extending Nginx recipe with .bbappend file while serving it as reverse proxy server for our application server.

tags:
  - Embedded
  - Yocto
  - BitBake
  - Nginx

comments: true
---

# Extend Nginx Service from OpenEmbedded Default Recipe

## Add Nginx in Layer Config

Nginx has default recipe (`.bb` file) and `files` defined by `openembedded`, so first you have to make sure that you have those files included. They should locate at `/meta-openembedded/meta-webserver/recipes-httpd/nginx` including `files` folder and several versions of `.bb` files.

If that's the case, you can simply add it in your `bblayers.conf`, like

```apacheconf 
BBLAYERS += "${BSPDIR}/sources/meta-openembedded/meta-webserver"
```

## Extend Nginx Default Settings

Since Nginx provides a convenient way to maintain and extend configuration by simply placing your custom setting inside specific folder (`/sites-enabled`, `/sites-available`), we can just adding some files without touching original recipe. (If you are unaware about what I just mentioned, I suggest to read the [official doc](https://www.nginx.com/resources/wiki/start/topics/examples/full/) or google *nginx sites-enabled*. There have been plenty of tutorials out there.)

To define out custom Nginx recipe, you should put the files under your meta layer like:
```
meta-mylayer/recipes-httpd/
└── nginx
    ├── files
    │   ├── custom-nginx.conf
    │   ├── nginx.service
    │   └── ssl
    │       ├── nginx.crt
    │       └── nginx.key
    └── nginx_1.20.1.bbappend
```

Here, I extend Nginx of version **1.20.1** with my server definition in `custom-nginx.conf` and a systemd service `nginx.service`.

---

Here is the example of `nginx_1.20.1.bbappend`:

```apacheconf 
FILESEXTRAPATHS:prepend := "${THISDIR}/files:"

SRC_URI += "file://custom-nginx.conf \
            file://ssl/ \
            file://nginx.service"

do_install:append() {
    # remove the example under /sites-enabled
    rm ${D}${sysconfdir}/nginx/sites-enabled/*
    install -m 0644 ${WORKDIR}/custom-nginx.conf ${D}${sysconfdir}/nginx/sites-enabled/custom-nginx.conf

    mkdir -p ${D}${sysconfdir}/nginx/ssl
    install -m 0644 ${WORKDIR}/ssl/nginx.crt ${D}${sysconfdir}/nginx/ssl/nginx.crt
    install -m 0600 ${WORKDIR}/ssl/nginx.key ${D}${sysconfdir}/nginx/ssl/nginx.key
    install -m 0644 ${WORKDIR}/nginx.service ${D}${systemd_system_unitdir}/nginx.service
}

# Add your custom configuration to nginx.conf
FILES:${PN} += "${sysconfdir}/nginx/sites-enabled/custom-nginx.conf"

# Define additional directories where SSL certificates may be stored
FILES:${PN} += "${sysconfdir}/nginx/ssl"

# Add SSL certificate and key files (modify the paths as needed)
FILES:${PN} += "${sysconfdir}/nginx/ssl/nginx.crt"
FILES:${PN} += "${sysconfdir}/nginx/ssl/nginx.key"

FILES:${PN} += "${systemd_system_unitdir}"
```

> Note that the example is based on **Yocto 4.0.x**. The syntax may differ for different version.

Don't forget to include these in the `layer.conf`