Important Notes

If you build with these device, kernel and vendor trees please use manifest-lineage.xml as your manifest.

You will also need a custom recovery which supports using /cust as /product. If you don't have one please
use the manifest-twrp.xml as your manifest for twrp.


Patches!

If you build lineage then apply the patches in the patches-lineage file. You can also use them if ROM does
not contain them.

If you build something different than lineage please do the following:
    1. Remove LiveDisplay
    2. Remove TrustHal
    3. If your compiling fails with error: no member named 'set_feedback' in 'struct amplifier_device'
       please apply this patch: 
       https://review.arrowos.net/c/ArrowOS/android_hardware_libhardware/+/10901 (Thx Franz Lopez)

If you are building with included gapps you may have to do this if you have not enough space in /product:
    1. You have to revert the /cust to /product patch. Here is the commit:
       https://github.com/alibei/android_kernel_xiaomi_sm6150-oss/commit/6f20f6d4d89dee04a8acf0bae7687316acdeb96d
    2. You have to remove the following in the sm6150-common tree:
          - In BoardConfig.mk remove the lines:  BOARD_PRODUCTIMAGE_PARTITION_SIZE := 872415232
                                                 BOARD_PRODUCTIMAGE_FILE_SYSTEM_TYPE := ext4
                                                 TARGET_COPY_OUT_PRODUCT := product
          - In fstab.com (default and emmc folder) remove the line:  /dev/block/bootdevice/by-name/cust
    3. You have to remove the following in the twrp device tree:
          - in recovery.fstab remove the line:  /product       ext4    /dev/block/bootdevice/by-name/cust
