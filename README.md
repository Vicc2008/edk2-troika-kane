# edk2-troika-kane
EDK II for Motorola One Action (Troika) Motorola One Vision (Kane)

## how to build
1.execute this command
```
sudo apt update
sudo apt install build-essential uuid-dev iasl git nasm python3-distutils gcc-aarch64-linux-gnu abootimg figlet
mkdir workspaceedk2
cd workspaceedk2
git clone https://github.com/tianocore/edk2.git -o 3a3713e62cfad00d78bb938b0d9fb1eedaeff314 --recursive --depth=1
git clone https://github.com/tianocore/edk2-platforms.git -o cfdc7f907d545b14302295b819ea078bc36c6a40 --recursive --depth=1
git clone https://github.com/edk2-troika-kane.git
. build_common.sh
GCC5_AARCH64_PREFIX=aarch64-linux-gnu- build -s -n 0 -a AARCH64 -t GCC5 -p TroikaPkg/TroikaPkg.dsc
gzip -c < workspace/Build/TroikaPkg/DEBUG_GCC5/FV/TROIKAPKG_UEFI.fd >uefi_img
cat troika.dtb >>uefi_img
abootimg --create uefi.img -k uefi_img -r ramdisk -f bootimg.cfg
rm -rf ./uefi_img
```
2.Debug and use
```
fastboot boot uefi.img
```
