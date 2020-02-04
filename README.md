# OSX-KVM: Cài đặt máy ảo OSX cho linux

1. Install QEMU

    * Ubuntu
    > sudo apt-get install qemu uml-utilities virt-manager dmg2img git wget libguestfs-tools virt-viewer

2. Chuẩn bị script

    * OSX-KVM
        > git clone https://github.com/kholia/OSX-KVM.git

3. Download MacOS base image

    * Run script
        > ./fetch-macOS.py

        ```
        #    ProductID    Version    Build   Post Date  Title
        1    061-26578    10.14.5  18F2059  2019-10-14  macOS Mojave
        2    061-26589    10.14.6   18G103  2019-10-14  macOS Mojave
        3    041-91758    10.13.6    17G66  2019-10-19  macOS High Sierra
        4    041-88800    10.14.4  18E2034  2019-10-23  macOS Mojave
        5    041-90855    10.13.5   17F66a  2019-10-23  Install macOS High Sierra Beta
        6    061-44345    10.15.2   19C39d  2019-11-15  macOS Catalina Beta
        7    061-44387    10.15.3    19D76  2020-01-28  macOS Catalina

        Choose a product to download (1-7): 
        ```

    * Lựa chọn phiên bản MacOS

4. Convert base image

    > qemu-img convert BaseSystem.dmg -O raw BaseSystem.img

    Hoặc

    > dmg2img BaseSystem.dmg BaseSystem.img

5. Tạo HDD ảo cài đặt OSX

    * Nếu phân vùng chứa hdd ảo định dạng btrfs nên dùng raw format

        > truncate -s 128G mac_hdd_ng.img

    * Nếu phân vùng chứa hdd ảo định dạng khác( ext, xfs, ...)

        > qemu-img create -f qcow2 mac_hdd_ng.img 128G

6. Cài đặt OSX

    * OSX Catalina

        * Get script: [qemu-osx-catalina](https://github.com/vinhlq/qemu-osx-catalina)

        * Run script
            > boot-macOS-Catalina-raw-hdd.sh
        
            hoặc
        
            > boot-macOS-Catalina-raw-hdd.sh

        * Remote: Sử dụng tool Remote Viewer(package virt-viewer)

        * URI: vnc://127.0.0.1:5900