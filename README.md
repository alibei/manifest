Important Notes

If you build with these device, kernel and vendor trees please use manifest-lineage.xml as your manifest.

You will also need a custom recovery which supports using /cust as /vendor. If you don't have one please
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
