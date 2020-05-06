![](https://github.com/relic-toolkit/relic/blob/master/art/rlc_logo.png)
=====

This is a version of [RELIC](https://github.com/relic-toolkit/relic) for the [ARM mbed](https://os.mbed.com/) platform.

### Notes

 * Only tested on [NUCLEO_F767ZI](https://os.mbed.com/platforms/ST-Nucleo-F767ZI/). Other platforms (with less RAM and flash) may not work.
 * Only tested with the `GCC_ARM` toolchain.
 * This version only builds the BN-254 pairing algorithms.
 * An insecure random number generator is used. On platforms which have a hardware TRNG (true random number generator), you can use [mbedtls](https://tls.mbed.org/kb/how-to/add-a-random-generator) for random number generation.
 * Arithmetic is done with the `easy` backend. It is possible to improve performance by using [GMP](https://singletonresearch.com/2017/07/11/cmake-and-gnu-multiple-precision-arithmetic-library-on-arm-cortex-m4/) on platforms that support it. For maximum performance one should write an assembly-optimized arithmetic backend.
 
### Build instructions
 
These instructions assume that you have a working installation of [mbed-cli](https://os.mbed.com/docs/mbed-os/latest/quick-start/offline-with-mbed-cli.html).
 
     git clone https://github.com/davidjao/relic
     cd relic
     mbed new .
     mbed compile
