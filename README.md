# UniXNU gs201 support

Shared Google Tensor G2 (gs201) support for UniXNU: CPU topology, GICv3,
watchdog, UFS, Mali G710 (Valhall CSF), ACPM and PMU resources, and the ABL
display pipeline registers.

`soc.toml` selects `ArmCpu` and `ArmDTPlatform`. Device repositories supply
memory layout, peripherals, firmware, power policy, and packaging.

## Evidence standard

Every register range and interrupt number in `dts/gs201.dtsi` carries a source
tag in its comment: `DTB` (decoded from the stock factory device tree,
rango BP4A.251205.006), `HW` (observed directly on panther silicon), or `TBD`
(placeholder, disabled). No value is guessed without saying so.

Notable silicon behavior recorded here:

- The stock bootloader enters the boot-image kernel through its PE32+ entry
  point with x0=x1=0, MMU on, an identity-limited mapping, and architectural
  timer reads trapped. Device-tree initrd handoff does not exist on this SoC.
- DSIM registers raise an external abort while the display block is
  clock-gated.
- PMU_ALIVE writes from EL1/EL2 are ignored; reset goes through SMC 0x82000504
  or the key-locked cluster watchdogs.

## Contents

| Path | Contents |
| --- | --- |
| `soc.toml` | SoC profile and component selection |
| `configs/gs201.config` | Kernel configuration fragment |
| `dts/gs201.dtsi` | Shared hardware resources |
| `patches/xnu/series` | Ordered SoC patches (empty: none yet) |
| `kits/` | Shared platform operations (pending: serial, ACPM ops, UFS ops) |

Build through the [UniXNU CLI](https://unixnu.com/building). Read the
[device repository specification](https://unixnu.com/porting/device-repository),
[device-tree specification](https://unixnu.com/porting/device-tree), and
[component catalog](https://unixnu.com/reference/components).

## Verified devices

| Board | Device repository | State |
| --- | --- | --- |
| panther (Google Pixel 7) | UniXNU-panther | SoC description and device record; firmware pending |
