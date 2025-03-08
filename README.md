# PCILeech RT5392 Firmware
PCILeech firmware, masquerading as a legal Ralink RT5392 device<br>
This firmware was created for my CypherCon 8 talk: [Not Fair!!1!: Bypassing Anti-Cheat With Direct Memory Access](https://cyphercon.com/presentation/not-fair1-bypassing-anti-cheat-with-direct-memory-access/).

![TeleScan output for flashed firmware](https://i.imgur.com/fr2u0AY.png)
![Drvscan-Interrupt-Info output](https://i.imgur.com/MMHiWFY.png)

## Features
- Shadow Configuration Space
  - Core needs to be modified, still presents as valid due to Type 0 CFG Space Header being built in IP Core prior to `EXT_CFG(_XP)_CAP_PTR` kicking in
- Writemask
- BAR Controller (Thank you [Dzul](https://github.com/dzul221/pcileech-Ralink-3090-/blob/main/src/pcileech_tlps128_bar_controller.sv) for the 3090 base)
  - Static BAR for the most part, loads EFUSE registers defined in rt2800pci driver
- Legacy INTx Interrupts (Thank you [Kilmu](https://github.com/kilmu1337/pcileech-csi2host/) for logic base)

## PCILeech Firmware Tree 🌲
List of files that have been changed from the original [pcileech-fpga](https://github.com/ufrisk/pcileech-fpga) repository.
- /ip/ Folder
  - [pcileech_cfgspace.coe](https://github.com/ret2c/pcileech-rt5392/blob/main/ip/pcileech_cfgspace.coe): Coefficient file that contains the configuration space for the firmware, allows you to mask the core to implement shadow space
  - [pcileech_cfgspace_writemask.coe](https://github.com/ret2c/pcileech-rt5392/blob/main/ip/pcileech_cfgspace_writemask.coe): Coefficient file that contains the writemask for the firmware, setting a permission map for which bits can be modified in the configuration space
- /pcie_7x/ Folder
  - [pcie_7x_0_core_top.v](https://github.com/ret2c/pcileech-rt5392/blob/main/pcie_7x/pcie_7x_0_core_top.v): Core file for defines the implementation for the PCIe endpoint interface. Includes core configuration, support for the device's capabilities (such as MSI(-x), AER, PM, DSN, etc.), clock management, and more. Since this firmware was already built from a .tcl, you can't recustomize the IP block through Vivado, you have to manually edit this file
- /src/ Folder
  - [pcileech_pcie_a7.sv](https://github.com/ret2c/pcileech-rt5392/blob/main/src/pcileech_pcie_a7.sv): Configuration file for physical PCIe signals, FIFO interfaces, etc. Main implementation is the inclusion of interrupt definitions to enable them
  - [pcileech_pcie_cfg_a7.sv](https://github.com/ret2c/pcileech-rt5392/blob/main/src/pcileech_pcie_cfg_a7.sv): Management for PCIe configuration space access and control, including R/W operations, device status, control registers, BAR tracking, and primarily (for our customization) interrupt functionality. Logic at the bottom is what sends an interrupt (`o_int`) through the wire
  - [pcileech_pcie_tlp_a7.sv](https://github.com/ret2c/pcileech-rt5392/blob/main/src/pcileech_pcie_tlp_a7.sv): Configuration file for TLP handling. Handles TLP processing, filtering, and routing. Main implementation is the inclusion of interrupt definitions to enable them
  - [pcileech_tlps128_bar_controller.sv](https://github.com/ret2c/pcileech-rt5392/blob/main/src/pcileech_tlps128_bar_controller.sv): PCIe BAR and PIO controller module. This file enables you to simulate behavior traits of the original donor card (RT5392 in this case). Since older Ralink chips are pretty easy to load the driver for, we only use static reads for the EFUSE logic seen in the original Linux driver code ([rt2800pci.c](https://github.com/torvalds/linux/blob/master/drivers/net/wireless/ralink/rt2x00/rt2800pci.c) & [rt2800.h](https://github.com/torvalds/linux/blob/master/drivers/net/wireless/ralink/rt2x00/rt2800.h)). Additionally, this file contains the logic to tell `pcileech_pcie_cfg_a7.sv` when to trigger an interrupt by implementing a counter that ticks per clock cycle
 
Realistically, you could configure each and every file within this repository for your intended purpose (like `tlp_magic` in `/src/pcileech_fifo.sv` for DNA Lock) but it's not necessary for getting a pass on [drvscan](https://github.com/Crump3tte/drvscan-interrupt-info).

## ❗ Disclaimer ❗
**Do not attempt to use this firmware with any cheating software.**

This firmware was created for security research, and I do not condone cheating in online multiplayer games. Additionally, this firmware is burned for being published publically, and most games have already blacklisted this Ralink chip. I will only support this for security research.

## Thank you to:
For support, guidance, and resources.
- [Simonrak](https://github.com/Simonrak/)
- [Desilvered](https://github.com/Silverr12)
- [Dzul](https://github.com/dzul221)
- [Kilmu](https://github.com/kilmu1337/)
- [Ekknod](https://github.com/ekknod/)
- [Ap3x](https://github.com/Ap3x/)
- [Ulf Frisk](https://github.com/ufrisk)
- Anybody else I've asked for help with debugging lol
