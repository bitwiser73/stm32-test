CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

set(PROJECT_NAME stm32-example-gpio-toggle)

ENABLE_LANGUAGE(ASM)

FIND_PACKAGE(CMSIS REQUIRED)
FIND_PACKAGE(STM32HAL COMPONENTS gpio tim REQUIRED)

#FIND_PACKAGE(STM32BSP REQUIRED)  # does not support the board yet
set(STM32BSP_INCLUDE_DIR ${STM32Cube_DIR}/Drivers/BSP/STM32L4xx_Nucleo_32)

INCLUDE_DIRECTORIES(
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMSIS_INCLUDE_DIRS}
    ${STM32HAL_INCLUDE_DIR}
    ${STM32BSP_INCLUDE_DIR}
    vendor/Inc
)

SET(PROJECT_SOURCES
    vendor/Src/main.c
    vendor/Src/stm32l4xx_it.c
    vendor/Src/system_stm32l4xx.c

    vendor/Src/startup_stm32l432xx.s
)

ADD_EXECUTABLE(
    ${PROJECT_NAME}
    ${PROJECT_SOURCES}
    ${STM32HAL_SOURCES}
)

ADD_CUSTOM_TARGET(
    flash_${PROJECT_NAME}
    ${TOOLCHAIN_PREFIX}/bin/arm-none-eabi-objcopy -O binary ${PROJECT_NAME} ${PROJECT_NAME}.bin
    COMMAND openocd -d0 -f \"${CMAKE_SOURCE_DIR}/openocd_l432kc.cfg\" -c \"init\;targets\;reset halt\;flash write_image erase $<TARGET_FILE_DIR:${PROJECT_NAME}>/${PROJECT_NAME}.bin 0x8000000;reset halt\;reset run\;shutdown\"
    DEPENDS ${PROJECT_NAME}
)

STM32_SET_TARGET_PROPERTIES(${PROJECT_NAME})
STM32_ADD_HEX_BIN_TARGETS(${PROJECT_NAME})
