# Agent instructions

This repository owns shared gs201 resources and platform operations.
Keep board peripherals, firmware selection, partition layout, and power
policy in the device repository. Preserve runtime source filenames,
classes, symbols, bundle IDs, and protocol IDs.

Read these UniXNU pages before editing:

1. [Porting](https://unixnu.com/porting/)
2. [Device repositories](https://unixnu.com/porting/device-repository)
3. [Components](https://unixnu.com/reference/components)
4. [Device trees](https://unixnu.com/porting/device-tree)
5. [Driver matching](https://unixnu.com/drivers/device-tree-matching)

gs201 is a Samsung Exynos-class SoC with no existing UniXNU or Mu-Silicium
platform: everything here is new. Do not copy Qualcomm register maps or
operations (RPMH, PDC, GENI, SMMU-500) into this repository — they describe
different silicon. Port sources are Google's gs kernel trees and the
linux-omarchy gs201 tree; check every address against `dts/gs201.dtsi` and
its evidence tags before use.

Every hardware value added here needs an evidence tag (`DTB`, `HW`, `TBD`)
and, for `HW`, the observation that produced it. Run builds from the UniXNU
checkout:

```sh
./unixnu defconfig panther_defconfig -D ../UniXNU-panther
./unixnu tree -D ../UniXNU-panther
```

Report commands, results, required local inputs, and hardware checkpoints.
Keep the documentation site in UniXNU. Write concise English describing
current behavior. Use direct statements and ordinary punctuation.
