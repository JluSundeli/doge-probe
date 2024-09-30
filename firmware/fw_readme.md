# Firmware readme

# Develop Environment
STM32CubeIDE
Version: 1.16.1
Build: 22882_20240916_0822 (UTC)

STM32G4xx HAL Driver version number V1.2.4

# project index

1. io_plan
2. usart_test

# How to config reset and boot pin in stm32G4 series

https://community.st.com/t5/stm32cubemx-mcus/how-we-should-do-to-configure-the-pg10-nrst-pin-as-nrst-we-just/td-p/304315

A:
```
As described in RM440:
8.3.16 Using PG10 as GPIO
    PG10 may be used as reset pin (NRST) or as a GPIO. Depending on the NRST_MODE bits in the user option byte, it switches to those mode:
    Reset input/output: default at power-on reset or after option bytes loading NRST_MODE = 3
    Reset input only: after option bytes loading NRST_MODE = 1
    GPIO PG10 mode: after option bytes loading NRST_MODE = 2

See description on the NRST pin in Section 6.1.2: System reset
```

B:
```
Is it something that's done through CubeMX?  If so, which rubric is it under?
Is this something I should call from my code?  Is there an code example?
What's the best practice?
I want to use the NRST as a reset input only.  nBOOT0 has a 10k pull-down.  Neither will be used as GPIO.
[I poked around CubeMX.  Tried to look it up on the web.  Searched the generated code for NRST_MODE.  But alas haven't found anything yet.]

```

C:
```
 This can be set in the option bytes, either via the STM32CubeProgrammer (function OB on the left) or from your code via the HAL function FLASH_OB_UserConfig or HAL_FLASHEx_OBProgram, for example. In most applications, however, the option bytes are programmed in production using the respective programmer.
```
