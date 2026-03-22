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

Workflow

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
select slot (_a or _b)
  ↓
normalize names
  ↓
7z recompress


---

Features

Supports A/B dynamic partition devices

Slot selection (_a or _b)

Removes duplicate partitions

Outputs slot-independent ROM set

Uses solid 7z compression (-ms=on)

No dependency on sparse conversion



---

Inputs

Name	Description

ARCHIVE_URL	Direct link to firmware archive
OUTPUT_NAME	Name of output .7z file
SLOT	Slot selection (_a or _b)



---

Requirements

Python 3

protobuf Python module

lpunpack.py (from unix3dgforce repo)

7z (p7zip)



---

Limitations

Only supports firmware with super.img

Does not process non-dynamic partition devices

Does not merge slots

Assumes partitions are valid and consistent

Compression gains are minimal for .img data



---

Notes

.img files are already high-entropy; recompression mainly reduces duplication (A/B)

Output size is typically ~50% of original super partition (due to slot removal)

Designed for extraction, not optimization



---

Example

Input:  firmware.zip (6 GB super)
Output: rom.7z (~3 GB, single slot)


---

Purpose

Create a minimal, clean ROM package from Android dynamic partitions without unnecessary duplication.
