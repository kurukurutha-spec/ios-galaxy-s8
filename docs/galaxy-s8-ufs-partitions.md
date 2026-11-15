# Galaxy S8 (SM-G950F) storage: UFS, not eMMC

Reported by the user (relayed from another assistant), **not yet verified on the phone from TWRP**:

- The S8 has UFS. There is no `/dev/block/mmcblk0p10`.
- BOOT: `/dev/block/platform/11120000.ufs/by-name/BOOT`, said to be `/dev/block/sda7`.

Do not trust any other `sdaN` number until it has been read from the phone. Check before writing anything:

```
adb shell ls -l /dev/block/platform/11120000.ufs/by-name/
adb shell blockdev --getsize64 /dev/block/platform/11120000.ufs/by-name/BOOT
```

Write BOOT only through the `by-name` path, and read it back and compare the SHA-256 against the image before rebooting.

Note: `A5XELTE_PROGRESS.md` and patches 0104-0108 describe the SM-A510F (eMMC, `mmcblk0p10`). Those paths do not apply to the S8.
