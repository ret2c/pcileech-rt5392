# PCILeech RT5392 Firmware
PCILeech firmware, masquerading as a legal Ralink RT5392 device

![TeleScan output for flashed firmware](https://i.imgur.com/fr2u0AY.png)

This firmware was created for my CypherCon talk: [Not Fair!!1!: Bypassing Anti-Cheat With Direct Memory Access](https://cyphercon.com/presentation/not-fair1-bypassing-anti-cheat-with-direct-memory-access/).<br>
It contains:
- Shadow Configuration Space
  - If you're tracking my commits for some reason, this current build has an incorrect **Message Lower Address** value
- Writemask (No RW1C Mask atm, sorry - will trip Gummybear detection)
- BAR Controller (Thank you [Dzul](https://github.com/dzul221/pcileech-Ralink-3090-/blob/main/src/pcileech_tlps128_bar_controller.sv) for the 3090 base)

❗ **Do not attempt to use this firmware with any cheating software** ❗<br>
This firmware was created for security research, and I do not condone cheating in online multiplayer games. Additionally, this firmware is burned for being published publically, and most games have already blocked this Ralink chip.

Creating this repo as a base right now, planning to publish this on 4/1.
