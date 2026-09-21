# COLLECTION-model4831

[![GitHub release](https://img.shields.io/github/release/mcci-catena/COLLECTION-model4831.svg)](https://github.com/mcci-catena/COLLECTION-model4831/releases/latest) [![GitHub commits](https://img.shields.io/github/commits-since/mcci-catena/COLLECTION-model4831/latest.svg)](https://github.com/mcci-catena/COLLECTION-model4831/compare/v0.2.0...master)

This repository contains the `COLLECTION` build system for the MCCI&reg; [Model 4831 Outdoor Environment Sensor](https://store.mcci.com/collections/remote-sensors/products/model-4831) production sketch.

- **Supported OS:** Linux (Ubuntu 18.04 or later recommended)

## Build Instructions

Follow the steps below to build the firmware:

1. Open Git Bash and clone this repository with submodules by executing the following command:

    ```bash
    git clone --recursive git@github.com:mcci-catena/COLLECTION-model4831.git
    ```

2. [`build-with-cli.sh`](build-with-cli.sh) script uses [`arduino-cli`](https://github.com/arduino/arduino-cli) to generate firmware builds for the `catena4618m201_simple` sketch. Use the following command to build:

    - to build with the test-signing key (`--test`):

      ```bash
      ./build-with-cli.sh --test --verbose
      ```

    - To perform a clean build:

      ```bash
      ./build-with-cli.sh --test --verbose --clean
      ```

3. The firmware can be built with various parameters. The following table shows available parameters to build the firmware.

    - Clock setting (`--clock`):

      | Value | Frequency |
      |--------|------------|
      | `2` | 2.097 MHz (no USB, least power) |
      | `4` | 4.194 MHz (no USB) |
      | `16` | 16 MHz |
      | `24` | 24 MHz |
      | `32` | 32 MHz (most power) |

    - Available Serial Configuration (`--serial`):

      | Option | Description |
      |------------|----------------|
      | `usb` | USB serial |
      | `hw` | Generic serial |
      | `none` | No serial |
      | `both` | USB + generic serial |

    - Available Regions (`--region`):

      | Region | Frequency Plan |
      |------------|----------------|
      | `us915` | North America 915 MHz |
      | `eu868` | Europe 868 MHz |
      | `au915` | Australia 915 MHz |
      | `as923` | Asia 923 MHz |
      | `as923jp` | Japan 923 MHz |
      | `kr920` | Korea 920 MHz |
      | `in866` | India 866 MHz |
      | `projcfg` | Uses `arduino-lmic/project_config/lmic_project_config_preconditions.h` |

    - Available Networks (`--network`):

      | Option | Network |
      |------------|----------------|
      | `ttn` | The Things Network |
      | `actility` | Actility ThingsPark |
      | `helium` | Helium |
      | `machineq` | machineQ |
      | `senet` | Senet |
      | `senra` | Senra |
      | `swisscom` | Swisscom |
      | `chirpstack` | ChirpStack |
      | `generic` | Generic LoRaWAN Network |
      | `projcfg` | Uses `arduino-lmic/project_config/lmic_project_config_preconditions.h` |

    - Available Subbands (`--subband`):

      | Option | Channels | Notes |
      |------------|-------------|----------------|
      | `default` | All | Works everywhere |
      | `sb0` | ch 0–7 | US / AU / CN470 |
      | `sb1` | ch 8–15 | US / AU / CN470 |
      | `sb2` | ch 16–23 | US / AU / CN470 |
      | `sb3` | ch 24–31 | US / AU / CN470 |
      | `sb4` | ch 32–39 | US / AU / CN470 |
      | `sb5` | ch 40–47 | US / AU / CN470 |
      | `sb6` | ch 48–55 | US / AU / CN470 |
      | `sb7` | ch 56–63 | US / AU / CN470 |
      | `sb8` | ch 64–71 | CN470 only |
      | `sb9` | ch 72–79 | CN470 only |
      | `sb10` | ch 80–87 | CN470 only |
      | `sb11` | ch 88–95 | CN470 only |

4. Some example build commands:

    - to build for 2 MHz clock and generic serial, for Europe, with the test-signing key:

      ```bash
      ./build-with-cli.sh --clock=2 --serial=hw --region=eu868 --test --verbose
      ```

    - to build for 32 MHz clock and USB serial, for India, with the test-signing key:

      ```bash
      ./build-with-cli.sh --clock=32 --serial=usb --region=in866 --test --verbose
      ```

    - to build for multiple regions and multiple networks with a single command:

      ```bash
      ./build-with-cli.sh --test --verbose && ./build-with-cli.sh --test --verbose --region=au915 --network=ttn && ./build-with-cli.sh --test --verbose --region=eu868 --network=ttn
      ```

5. After a successful build, firmware artifacts are generated in `COLLECTION-model4831/build`. Use the command `ls -CF build` to verify the build files. Example usage given below.

      ```bash
      $ ls -CF build
      model4831-v0.5.0-ttn-us915-default-clk16-serusb-mcci_test/  model4831-v0.5.0-ttn-au915-default-clk16-serusb-mcci_test/
      model4831-v0.5.0-ttn-eu868-default-clk16-serusb-mcci_test/
      $
      ```

    - The directory names are structured in a consistent way to reflect the build configuration:
      - `outputname-version-network-region-subband-clock-serial-codekey`

6. The build directory includes two subdirectories.

    - `boot`, which contains the bootloader build directory.
    - `ide`, which contains the application build directory.

7. The `ide` directory contains a number of files. The important files have the build configuration as part of their name.

    | Name                                      | Description
    |-------------------------------------------|-----------------
    | catena4618m201_simple-bootloader-_release_.dfu | The combined bootloader and app, in DfuSe format.
    | catena4618m201_simple-bootloader-_release_.hex | The combined bootloader and app, in Intel hex format.
    | catena4618m201_simple.ino-_release_.bin        | The signed application in binary format (used for uploads with the SPT)
    | catena4618m201_simple.ino-_release_.dfu        | The signed application in DFU format.
    | catena4618m201_simple.ino-_release_.elf        | The signed application in ELF format.
    | catena4618m201_simple.ino-_release_.hex        | The signed application in Intel hex format.
    | McciBootloader_46xx-_release_.bin        | The signed bootloader in binary format.
    | McciBootloader_46xx-_release_.elf        | The signed bootloader in ELF format.
    | McciBootloader_46xx-_release_.hex        | The signed bootloader in Intel hex format.

---

## Meta

### Trademarks and copyright

MCCI and MCCI Catena are registered trademarks of MCCI Corporation. LoRa is a registered trademark of Semtech Corporation. LoRaWAN is a registered trademark of the LoRa Alliance.

This document and the contents of this repository are copyright 2021-2026, MCCI Corporation.

### License

This repository is released under the [MIT](./LICENSE) license. Commercial licenses are also available from MCCI Corporation.

### Support Open Source Hardware and Software

MCCI invests time and resources providing this open source code, please support MCCI and open-source hardware by purchasing products from MCCI, Adafruit and other open-source hardware/software vendors!

For information about MCCI's products, please visit [store.mcci.com](https://store.mcci.com/).