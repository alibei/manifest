Important Notes

If you build with these device, kernel and vendor trees please use manifest-lineage.xml as your manifest.

You will also need a custom recovery which supports using /cust as /product. If you don't have one please
use the manifest-twrp.xml as your manifest for twrp.

Patches!

If you build lineage then apply the patches in the patches-lineage file. You can also use them if ROM does
not contain them. If your ROM does not contain them you have to patch it manually or you leave them out because
they are not needed for a working FOD.

If you build something different than lineage please do the following:
 - Remove LiveDisplay
 - Remove TrustHal

If your compiling fails with error: no member named 'set_feedback' in 'struct amplifier_device' please apply this patch:      
 - https://review.arrowos.net/c/ArrowOS/android_hardware_libhardware/+/10901 (Thx Franz Lopez)

If you are building and getting the error that you don't have enough space in /product:

You have to revert the /cust to /product patch. Here is the commit:
 - https://github.com/alibei/android_kernel_xiaomi_sm6150-oss/commit/6f20f6d4d89dee04a8acf0bae7687316acdeb96d

You have to remove the following in the sm6150-common tree:

In BoardConfig.mk remove the lines:
 - BOARD_PRODUCTIMAGE_PARTITION_SIZE := 872415232
 - BOARD_PRODUCTIMAGE_FILE_SYSTEM_TYPE := ext4
 - TARGET_COPY_OUT_PRODUCT := product

In fstab.com (default and emmc folder) remove the line:
 - /dev/block/bootdevice/by-name/cust

You have to remove the following in the twrp device tree:
 - in recovery.fstab remove the line:  /product       ext4    /dev/block/bootdevice/by-name/cust
