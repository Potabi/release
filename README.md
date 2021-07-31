# release
A place for the project to host ISO files, changelogs and more.


## Creating an ISO (instructions) 
1. Build src
    ```sh
    make buildworld buildkernel -j8 
    cd release
    make obj
    make real-release NODOCS=1 NOSRC=1 NOPORTS=1
    ```
1. Extract ISO contents
    ```sh
    mkdir -p ~/iso
    cp /usr/obj/usr/src/amd64.amd64/release/disc1.iso ~/iso/.
    cd ~/iso
    7z x disc1.iso && rm disc1.iso
    ```
1. Install packages from package manager
    ```sh
    pkg -r ~/iso install mate xorg xterm # more
    ```
