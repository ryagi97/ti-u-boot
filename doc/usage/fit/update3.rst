.. SPDX-License-Identifier: GPL-2.0+

Automatic software update: multiple files
=========================================

::

    /dts-v1/;

    / {
        description = "Automatic software updates: kernel, ramdisk, FDT";
        #address-cells = <1>;

        images {
            update-1 {
                description = "Linux kernel binary";
                data = /incbin/("./vmlinux.bin.gz");
                compression = "none";
                type = "firmware";
                load = <FF700000>;
                hash-1 {
                    algo = "sha256";
                };
            };
            update-2 {
                description = "Ramdisk image";
                data = /incbin/("./ramdisk_image.gz");
                compression = "none";
                type = "firmware";
                load = <FF8E0000>;
                hash-1 {
                    algo = "sha256";
                };
            };

            update-3 {
                description = "FDT blob";
                data = /incbin/("./blob.fdt");
                compression = "none";
                type = "firmware";
                load = <FFAC0000>;
                hash-1 {
                    algo = "sha256";
                };
            };
        };
    };
