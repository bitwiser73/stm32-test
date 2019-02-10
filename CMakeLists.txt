CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

option(STM32Cube_DIR "STM32 Cube root directory")
option(TOOLCHAIN_PREFIX "Toolchain root directory")

add_subdirectory(stm32-example/GPIO_IOToggle)
add_subdirectory(stm32-example/SPI_FullDuplex_ComPolling)
