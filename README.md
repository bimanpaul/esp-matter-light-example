# Light

This example creates a Color Temperature Light device using the ESP
Matter data model.

See the [docs](https://docs.espressif.com/projects/esp-matter/en/latest/esp32/developing.html) for more information about building and flashing the firmware.

# Requirements
    
    Host: Ubuntu 20.04 or 22.04
    Repository: esp-idf, esp-matter, connectedhomeip
    Board: ESP32-C6-DevKitM-1
    Testing: ST-App, WCH (Hub V3 or Harman Speaker is also fine), WiFi (Open Internet)

# Host Setup

You should install drivers and support packages for your development host. Linux is a supported development hosts for Matter, the recommended host versions are:
Ubuntu 20.04 or 22.04 LTS

# Setup esp-idf SDK

## Install Prerequisites for esp-idf

In order to use ESP-IDF with the ESP32, you need to install some software packages based on your Operating System. To compile using ESP-IDF you will need to get the following packages. The command to run depends on which distribution of Linux you are using:

Ubuntu and Debian:

    sudo apt-get install git wget flex bison gperf python3 \
        python3-venv cmake ninja-build ccache libffi-dev \
        libssl-dev dfu-util libusb-1.0-0

- CMake version 3.16 or newer is required for use with ESP-IDF. Run “tools/idf_tools.py install cmake” to install a suitable version if your OS versions doesn’t have one.

- If you do not see your Linux distribution in the above list then please check its documentation to find out which command to use for package installation.

## Getting the Repository esp-idf

    git clone --recursive https://github.com/espressif/esp-idf.git
    cd esp-idf; git checkout v5.2.1; git submodule update --init --recursive;
    ./install.sh
    cd ..

## Configuring the Environment

This should be done each time a new terminal is opened

    cd esp-idf; source ./export.sh; cd ..

# ESP Matter Setup

There are two options to setup esp-matter, you can select one according to demand:
- ESP matter repository, including esp-matter SDK and tools (e.g., CHIP-tool, CHIP-cert, ZAP, …).
- ESP matter component, including esp-matter SDK.

## Installing prerequisites for Linux

On Debian-based Linux distributions such as Ubuntu, these dependencies can be satisfied with the following command:

    sudo apt-get install git gcc g++ pkg-config libssl-dev libdbus-1-dev \
         libglib2.0-dev libavahi-client-dev ninja-build python3-venv python3-dev \
         python3-pip unzip libgirepository1.0-dev libcairo2-dev libreadline-dev

### UI builds

If building -with-ui variant, also install SDL2:

    sudo apt-get install libsdl2-dev

## ESP-Matter Repository

Cloning the esp-matter repository takes a while due to a lot of submodules in the upstream connectedhomeip, so if you want to do a shallow clone use the following command:

    cd esp-idf
    source ./export.sh
    cd ..
    git clone --depth 1 https://github.com/espressif/esp-matter.git
    cd esp-matter
    git submodule update --init --depth 1
    cd ./connectedhomeip/connectedhomeip
    ./scripts/checkout_submodules.py --platform esp32 linux --shallow
    cd ../..
    ./install.sh
    cd ..

As of writing (dated May 17, 2024 ), the HEAD or latest code of esp-matter is having some issue. This issue may be fixed in future.

Author has tested with below commit on Ubuntu 22.04 & Ubuntu 20.04.

    commit bd3cadcf25944aaf709879fd4bb3f957e0d64894 (HEAD -> main)
    Author: Shubham Patil shubham.patil@espressif.com
    Date: Thu Jan 11 20:18:17 2024 +0530
    indent the code

Command Sequences are given below which used a specific commit.

    cd esp-idf
    source ./export.sh
    cd ..
    #Full clone
    git clone https://github.com/espressif/esp-matter.git
    cd esp-matter
    #Reset to a Specific Commit
    git reset --hard bd3cadcf25944aaf709879fd4bb3f957e0d64894
    git submodule update --init --depth 1
    cd ./connectedhomeip/connectedhomeip
    ./scripts/checkout_submodules.py --platform esp32 linux --shallow
    cd ../..
    ./install.sh
    cd ..

 
### Configuring the Environment

This should be done each time a new terminal is opened

    cd esp-idf; source ./export.sh; cd ..
    cd esp-matter; source ./export.sh; cd ..
