cmake_minimum_required(VERSION 3.10)

file(GLOB SOURCES src/littlefs/*.c)
list(APPEND SOURCES
    src/lfs_config.c
    src/esp_littlefs_abs.c
    src/esp_littlefs_flash.c
    src/esp_littlefs_ram.c
    src/esp_littlefs_sdcard.c
    src/esp_littlefs_vfs.c
    src/littlefs/lfs.c
    src/littlefs/lfs_util.c
    )

idf_component_register(
    SRCS ${SOURCES}
    INCLUDE_DIRS include
    PRIV_INCLUDE_DIRS src
    REQUIRES spi_flash sdmmc vfs
    PRIV_REQUIRES esptool_py
    )

set_source_files_properties(
    ${SOURCES}
    PROPERTIES COMPILE_FLAGS "-DLFS_CONFIG=lfs_config.h"
)
