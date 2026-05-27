# Marlin CFW

This is a guide to install Marlin firmware for the BTT SKR MINI E3 V3 (on Linux).

## Configuration

The `.h` files have been modified for my usage (Sherpa Mini extruder, etc.). Sample configurations can be found at [MarlinFirmware/Configurations](https://github.com/MarlinFirmware/Configurations/).

### Sherpa mini (LDO)

Depending of the type of motor you have installed (LDO-36STH17 / LDO-36STH20) you need to change the current in Configuration_adv.h to max 0.35A / max 1A. Currently set to default 680mA.

## Steps

- Download [VSCode](https://code.visualstudio.com/)
- Install the Auto Build Marlin extension
- Install the PlatformIO IDE extension

Download the latest Marlin firmware release from [marlinfw.org](https://marlinfw.org/meta/download/) and unzip it.

Open VSCode from the downloaded repository.

In the PlatformIO page, click on "Open Project" and select the extracted Marlin folder.

### Files to change

- In `platformio.ini`, replace `default_envs` from the start of the file with `default_envs = STM32G0B1RE_btt`
- Delete `-Wl,--no-warn-rwx-segment` from `platformio.ini` in the `[env:STM32G0B1RE_btt]` scope
- Delete `-Wl,--no-warn-rwx-segment` from `ini/stm32g0.ini` in the `[env:STM32G0B1RE_btt]` scope
- In `ini/stm32g0.ini`, replace the segment which starts with `[env:STM32G0B1RE_btt]` with the following:

```
[env:STM32G0B1RE_btt]
extends = stm32_variant
platform = ststm32@~14.1.0
platform_packages = framework-arduinoststm32@https://github.com/stm32duino/Arduino_Core_STM32/archive/refs/tags/2.6.0.zip
```

`platformio lib install marlinfirmware/U8glib-HAL`  <-- Don't know if this is needed

In the Auto Build Marlin extension, click on Build.
