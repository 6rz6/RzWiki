## How To solve errors in ext4.vhdx while moving or mounting WSL2 distro (docker-desktop-data in my case)
 
* ###  WSL2: Process cannot access the file because it is being used by another process
* ###  Can't mount ext4 partition (error 0x80070020 - the file is being used by another process)
* ###  Error code: Wsl/Service/AttachDisk/WSL_E_ELEVATION_NEEDED_TO_MOUNT_DISK

1. Make sure in the windows disk partition manager the ext4.vhdx in unmounted (might appear as "disk2")
2. in cmd shutdown wsl: `wsl --shutdown`
3. check all the wsl distros are stopped : `D:\Docker\wsl\distro>wsl -l -v`
 ` NAME                   STATE           VERSION`
`* Ubuntu                 Stopped         2`
`  docker-desktop-data    Stopped         2`
`  docker-desktop         Stopped         2`
4. Copy the ext4.vhdx to the new drive for example `d:/docker/wsl/distro`
5. Terminate docker-desktop-data `wsl --terminate docker-desktop-data'
6. Unregister the old ext4.vhdx: `wsl --unregister docker-desktop-data ext4.vhdx`
7. change dir and go to the new location of the vhdx file 
8. mount the distro in the new location: 'wsl --mount ext4.vhdx'
9. import it using: `wsl --import-in-place docker-desktop-data ext4.vhdx`
10. Restart the wsl in cmd 
11. Restart Docker desktop in windows
12. check all the distros are back online: `D:\Docker\wsl\distro> wsl -l -v`
`  NAME                   STATE           VERSION`
`* Ubuntu                 Running         2`
` docker-desktop-data    Running         2`
` docker-desktop         Running         2`
