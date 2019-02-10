# Experiments with Nucleo32 STM32L432KC

![nucleo-l432kc](https://www.st.com/content/ccc/fragment/product_related/rpn_information/board_photo/group0/4a/65/08/ad/7e/5b/41/1a/ulp_nucleo-32-qfn32/files/ulp_nucleo-32-qfn32.jpg/_jcr_content/translations/en.ulp_nucleo-32-qfn32.jpg)

[nucleo-l432kc](https://www.st.com/content/st_com/en/products/evaluation-tools/product-evaluation-tools/mcu-eval-tools/stm32-mcu-eval-tools/stm32-nucleo-boards/nucleo-l432kc.html)

## Requirements
- ubuntu 18.10
- cmake
- [stm32cubel4](https://www.st.com/content/st_com/en/products/embedded-software/mcus-embedded-software/stm32-embedded-software/stm32cube-mcu-packages/stm32cubel4.html) from STMicroelectronics (en.stm32cubel4.zip)
- [toolchain](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads/7-2018-q2-update)
- openocd (to be able to flash)

## Build instructions
After editing configure-cmake

```bash
mkdir build
cd build
../configure-cmake ..
make
```

## Flash an example into the board
```bash
make flash_stm32-example-gpio-toggle
```

![nucleo-l432kc-pin](https://community.st.com/sfc/servlet.shepherd/version/renditionDownload?rendition=ORIGINAL_Png&versionId=0680X000006qNs2&operationContext=CHATTER&contentId=05T0X00000NPL0H)
