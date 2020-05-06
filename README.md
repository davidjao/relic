![](https://github.com/relic-toolkit/relic/blob/master/art/rlc_logo.png)
=====

This is a version of [RELIC](https://github.com/relic-toolkit/relic) for the [ARM mbed](https://os.mbed.com/) platform.

### Notes

 * Only tested on [NUCLEO_F767ZI](https://os.mbed.com/platforms/ST-Nucleo-F767ZI/). Other platforms (with less RAM and flash) may not work. See build output (below) for details on RAM / flash consumption.
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

This version does not build using the online mbed compiler, since it uses features such as `.mbedignore` which are not supported on the online compiler.

### Build output

    Link: relic
    Elf2Bin: relic
    | Module             |      .text |    .data |          .bss |
    |--------------------|------------|----------|---------------|
    | [fill]             |    144(+0) |   11(+0) |        22(+0) |
    | [lib]/c.a          |  26000(+0) | 2472(+0) |        89(+0) |
    | [lib]/gcc.a        |    768(+0) |    0(+0) |         0(+0) |
    | [lib]/misc         |    180(+0) |    4(+0) |        28(+0) |
    | mbed-os/components |    162(+0) |    0(+0) |         0(+0) |
    | mbed-os/drivers    |    244(+0) |    0(+0) |         0(+0) |
    | mbed-os/events     |   1504(+0) |    0(+0) |      3108(+0) |
    | mbed-os/features   |   2166(+0) |    0(+0) |     12796(+0) |
    | mbed-os/hal        |   1666(+0) |    8(+0) |       130(+0) |
    | mbed-os/platform   |   4590(+0) |  260(+0) |       221(+0) |
    | mbed-os/rtos       |  10560(+0) |  168(+0) | 34908(+16384) |
    | mbed-os/targets    |  13058(+0) |    5(+0) |      1262(+0) |
    | src/arch           |      4(+0) |    0(+0) |         0(+0) |
    | src/bn             |   4692(+0) |    0(+0) |         0(+0) |
    | src/dv             |    144(+0) |    0(+0) |         0(+0) |
    | src/ep             |   6758(+0) |    0(+0) |         0(+0) |
    | src/epx            |   6356(+0) |    0(+0) |         0(+0) |
    | src/fp             |   3202(+0) |    0(+0) |         0(+0) |
    | src/fpx            |  26038(+0) |    0(+0) |         0(+0) |
    | src/low            |   6124(+0) |    0(+0) |         0(+0) |
    | src/md             |    844(+0) |   32(+0) |         0(+0) |
    | src/pp             |  19130(+0) |    0(+0) |         0(+0) |
    | src/rand           |    800(+0) |    0(+0) |         0(+0) |
    | src/relic_core.o   |    100(+0) |    0(+0) |     14220(+0) |
    | src/relic_test.o   |     24(+0) |    0(+0) |         0(+0) |
    | src/relic_util.o   |     70(+0) |    0(+0) |         0(+0) |
    | test/test_pp.o     |  15768(+0) |    0(+0) |         0(+0) |
    | Subtotals          | 151096(+0) | 2960(+0) | 66784(+16384) |
    Total Static RAM memory (data + bss): 69744(+16384) bytes
    Total Flash memory (text + data): 154056(+0) bytes
    
    Image: ./BUILD/NUCLEO_F767ZI/GCC_ARM/relic.bin

### Console output

    -- Tests for the PP module
    
    -- Curve BN-P254:
    
    ** Arithmetic
    
    Testing if miller doubling is correct...                                      [PASS]
    Testing if miller doubling in affine coordinates is correct...                [PASS]
    Testing if miller doubling in projective coordinates is correct...            [PASS]
    Testing if basic projective miller doubling is correct...                     [PASS]
    Testing if lazy-reduced projective miller doubling is consistent...           [PASS]
    Testing if miller addition is correct...                                      [PASS]
    Testing if miller addition in affine coordinates is correct...                [PASS]
    Testing if miller addition in projective coordinates is correct...            [PASS]
    Testing if basic projective miller addition is consistent...                  [PASS]
    Testing if lazy-reduced projective miller addition is consistent...           [PASS]
    Testing if pairing non-degeneracy is correct...                               [PASS]
    Testing if pairing is bilinear...                                             [PASS]
    Testing if multi-pairing is correct...                                        [PASS]
    Testing if tate pairing non-degeneracy is correct...                          [PASS]
    Testing if tate pairing is bilinear...                                        [PASS]
    Testing if tate multi-pairing is correct...                                   [PASS]
    Testing if weil pairing non-degeneracy is correct...                          [PASS]
    Testing if weil pairing is bilinear...                                        [PASS]
    Testing if optimal ate pairing non-degeneracy is correct...                   [PASS]
    Testing if optimal ate pairing is bilinear...                                 [PASS]
    Testing if optimal ate multi-pairing is correct...                            [PASS]
    
    -- All tests have passed.
