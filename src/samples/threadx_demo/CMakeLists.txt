# Licensed under the MIT License.

cmake_minimum_required(VERSION 3.20 FATAL_ERROR)

set(ROOT_DIR ${CMAKE_SOURCE_DIR}/../../..)

list(APPEND CMAKE_MODULE_PATH ${ROOT_DIR}/cmake)

include(variables)
include(utilities)

# Define the Project
# CXX enables IntelliSense only. Sources are still compiled as C.
project(threadx_demo C CXX ASM)

set(SOURCES
    main.c
)

add_executable(${PROJECT_NAME} ${SOURCES})

add_subdirectory(${LIB_DIR} lib)

target_link_libraries(${PROJECT_NAME}
    azrtos::threadx

    stm32cubef4
    mxchip_bsp
    wiced_sdk
)

set_target_linker(${PROJECT_NAME} ${AZ3166_DIR}/startup/MXChip_AZ3166.ld)

post_build(${PROJECT_NAME})