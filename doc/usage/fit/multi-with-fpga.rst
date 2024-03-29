.. SPDX-License-Identifier: GPL-2.0+

Multiple kernels, ramdisks and FDT blobs with FPGA
==================================================

This example makes use of the 'loadables' field::

    /dts-v1/;

    / {
        description = "Configuration to load fpga before Kernel";
        #address-cells = <1>;

        images {
            fdt-1 {
                description = "zc706";
                data = /incbin/("/tftpboot/devicetree.dtb");
                type = "flat_dt";
                arch = "arm";
                compression = "none";
                load = <0x10000000>;
                hash-1 {
                    algo = "sha256";
                };
            };

            fpga {
                description = "FPGA";
                data = /incbin/("/tftpboot/download.bit");
                type = "fpga";
                arch = "arm";
                compression = "none";
                load = <0x30000000>;
                compatible = "u-boot,fpga-legacy"
                hash-1 {
                    algo = "sha256";
                };
            };

            linux_kernel {
                description = "Linux";
                data = /incbin/("/tftpboot/zImage");
                type = "kernel";
                arch = "arm";
                os = "linux";
                compression = "none";
                load = <0x8000>;
                entry = <0x8000>;
                hash-1 {
                    algo = "sha256";
                };
            };
        };

        configurations {
            default = "config-2";
            config-1 {
                description = "Linux";
                kernel = "linux_kernel";
                fdt = "fdt-1";
            };

            config-2 {
                description = "Linux with fpga";
                kernel = "linux_kernel";
                fdt = "fdt-1";
                loadables = "fpga";
            };
        };
    };
