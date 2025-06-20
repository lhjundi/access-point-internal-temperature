# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Initialise pico_sdk from installed location
# (note this can come from environment, CMake cache etc)

# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.1.1)
set(toolchainVersion 14_2_Rel1)
set(picotoolVersion 2.1.1)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
set(PICO_BOARD pico_w CACHE STRING "Board type")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(access-point-internal-temperature C CXX ASM)

# Initialise the Raspberry Pi Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

add_executable(
    access-point-internal-temperature 
    access-point-internal-temperature.c
    dhcpserver/dhcpserver.c
    dnsserver/dnsserver.c)

pico_set_program_name(access-point-internal-temperature "access-point-internal-temperature")
pico_set_program_version(access-point-internal-temperature "0.1")

# Modify the below lines to enable/disable output over UART/USB
pico_enable_stdio_uart(access-point-internal-temperature 1)
pico_enable_stdio_usb(access-point-internal-temperature 1)

# Add the standard library to the build
target_link_libraries(access-point-internal-temperature
        pico_stdlib
        hardware_adc
        hardware_gpio
        pico_stdio_usb
        pico_cyw43_arch_lwip_threadsafe_background)

# Add the standard include files to the build
target_include_directories(access-point-internal-temperature PRIVATE
        ${CMAKE_CURRENT_LIST_DIR}
        ${CMAKE_CURRENT_LIST_DIR}/.. #for our common lwipopts
        ${CMAKE_CURRENT_LIST_DIR}/dhcpserver
        ${CMAKE_CURRENT_LIST_DIR}/dnsserver
)

pico_configure_ip4_address(
    access-point-internal-temperature PRIVATE
    CYW43_DEFAULT_IP4_ADDRESS 192.168.4.1)

# Add any user requested libraries
target_link_libraries(access-point-internal-temperature 
        
        )

pico_add_extra_outputs(access-point-internal-temperature)

