# Marlin CFW

Small guide to install Marlin CFW for BTT SKR MINI E3 V3 (on linux)

## Configuration

The .h have been modified for my usage (sherpa mini extruder, etc...)
Samples are found here https://github.com/MarlinFirmware/Configurations/

## Steps

- Download vscode  
- Download Auto Build Marlin from vscode 
- Download PlatformIO IDE from vscode 

Download Marlin FW latest release https://marlinfw.org/meta/download/ and unzip it.

Open vscode from the downloaded repository.

On vscode PlatformIO page, click on "Open Project", and select the the extracted Marlin FW folder

### Files to change

- In platformio.ini, replace the default_envs from the start of the file with `default_envs = STM32G0B1RE_btt`
- Delete `-Wl,--no-warn-rwx-segment` from platformio.ini in the `[env:STM32G0B1RE_btt]` scope  
- Delete `-Wl,--no-warn-rwx-segment` from ini/stm32g0.ini in the `[env:STM32G0B1RE_btt]` scope  
- In ini/stm32g0.ini, replace the segment wich start with [env:STM32G0B1RE_btt] with the following :
```
[env:STM32G0B1RE_btt]
extends = stm32_variant
platform = ststm32@~14.1.0
platform_packages = framework-arduinoststm32@https://github.com/stm32duino/Arduino_Core_STM32/archive/refs/tags/2.6.0.zip
```

`platformio lib install marlinfirmware/U8glib-HAL` <-- Don't know if this is needed

On the auto build Marlin extension, click on build. Hopefully it works
