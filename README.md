# PCILeech RT5392 Firmware
PCILeech firmware, masquerading as a legal Ralink RT5392 device<br>
This firmware was created for my CypherCon 8 talk: [Not Fair!!1!: Bypassing Anti-Cheat With Direct Memory Access](https://cyphercon.com/presentation/not-fair1-bypassing-anti-cheat-with-direct-memory-access/).

![TeleScan output for flashed firmware](https://i.imgur.com/fr2u0AY.png)

## Features
- Shadow Configuration Space
  - If you're tracking my commits for some reason, this current build has an incorrect **Message Lower Address** value
- Writemask (No RW1C Mask atm, sorry - will trip Gummybear detection)
- BAR Controller (Thank you [Dzul](https://github.com/dzul221/pcileech-Ralink-3090-/blob/main/src/pcileech_tlps128_bar_controller.sv) for the 3090 base)

You will not be able to recustomize the IP Block with this, stick to Shadow CFG. Edit `/pcie_7x/pcie_7x_0_core_top.v` with your chosen configurations.

## ❗ Disclaimer ❗
**Do not attempt to use this firmware with any cheating software.**

This firmware was created for security research, and I do not condone cheating in online multiplayer games. Additionally, this firmware is burned for being published publically, and most games have already blocked this Ralink chip. I will only support this for security research.

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
