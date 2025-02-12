# PCILeech RT5392
PCILeech firmware, masquerading as legal Ralink RT5392 device

This firmware was created for my CypherCon talk: [Not Fair!!1!: Bypassing Anti-Cheat With Direct Memory Access](https://cyphercon.com/presentation/not-fair1-bypassing-anti-cheat-with-direct-memory-access/).<br>
It contains:
- Shadow Configuration Space
- Writemask (RW1C Mask when I have time)
  - It causes Gummybear detection in its current state
- BAR Controller (Thank you [Dzul](https://github.com/dzul221/pcileech-Ralink-3090-/blob/main/src/pcileech_tlps128_bar_controller.sv) for the 3090 base)

Creating this repo as a base right now, planning to publish this on 4/1.
