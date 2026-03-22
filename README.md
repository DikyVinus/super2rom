# super2rom

Extract Android dynamic partitions from `super.img`, select a single A/B slot, and repackage into an optimized `.7z` archive.

---

## Overview

`super2rom` processes Android firmware packages by:

1. Extracting `super.img` from firmware
2. Unpacking dynamic partitions using `lpunpack`
3. Selecting a single slot (`_a` or `_b`)
4. Normalizing partition names (removing slot suffix)
5. Repacking selected partitions into a compressed `.7z`

---

## Output

Produces a clean ROM archive containing only:

```text
system.img
vendor.img
product.img
system_ext.img
odm.img
system_dlkm.img
vendor_dlkm.img
odm_dlkm.img
vbmeta_system.img
vbmeta_vendor.img
```

---

### Tutorial (GitHub Actions)

1. Fork the repository

Go to your repository page

Click Fork

This creates your own copy



---

2. Enable Actions

Go to Actions tab

If prompted, enable workflows



---

3. Run the workflow

Open Actions

Select: Firmware ROM Extractor (Optimized 7z)

Click Run workflow


Fill inputs:

ARCHIVE_URL → direct raw firmware link

OUTPUT_NAME → output name (e.g. rom)

SLOT → _a or _b



---

4. Wait for completion

Workflow runs on GitHub runner

Takes ~5–15 minutes depending on firmware size



---

5. Download result

Go to Releases

Find latest run (tag = run ID)

Download .7z file



---

### Workflow Pipeline

firmware.zip
  ↓
extract
  ↓
super.img
  ↓
lpunpack
  ↓
partition_a / partition_b
  ↓
select slot
  ↓
normalize names
  ↓
7z recompress


---

### Inputs

Name	Description

ARCHIVE_URL	Direct link to firmware archive
OUTPUT_NAME	Name of output .7z file
SLOT	Slot selection (_a or _b)



---

### Requirements

Handled automatically in workflow:

Python 3

protobuf

p7zip

lpunpack (Python script)



---

### Limitations

Requires super.img (dynamic partition devices only)

Does not support non-A/B devices

Does not merge slots

.img compression gains are minimal



---

### Notes

Size reduction comes from removing duplicate A/B partitions

Recompression does not significantly shrink .img

Output is intended for modification or repacking



---

### Example

Input:  firmware.zip (~6 GB super)
Output: rom.7z (~3 GB, single slot)


---

### Purpose

Generate a clean, slot-specific ROM package from Android dynamic partitions without duplication.
