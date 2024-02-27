# Machinist X99-MR9A/E5-MR9A
Repo with resources related to the motherboard in question.

## Specifications
|Spec | Details  |
|--|--|
|Brand  |Machinist |
| Model | X99-MR9A/E5-MR9A (see below) |
| Socket | LGA2011-3
| Size | ATX |
| Chipset | C226/B85/Q87 |
| Memory | 4x DDR4, quad channel, max 128GB |
| LAN | 1Gbps |
| PCI-E | 2x x16, 1x x4, 1x x1 |
| M.2 | 1x NVMe, 1x NGFF/SATA |
| SLI/CrossFireX | not supported |

## Pros and cons
Pros: good VRM section - [triplet MOSFETs](https://xeon-e5450.ru/socket-2011-3/machinist-x99-mr9a/), properly cooled with a big heatsink; working sleep mode; PCI-E ports connected directly to the CPU (aside from the x1 port); 

Cons: invalid sensor readings; low-quality original BIOS; no overclocking capabilities; smart fan only works for CPU_FAN1 (and only for 4-pin coolers!); no SLI/CrossFireX


## Revisions
Supposedly a revision with dedicated buttons for power, reset and a POST code screen exists, although most if not all known MR9As in the wild do not have these features. The layout of the board seems practically identical to the "standard" MR9A with the small difference of the buzzer being located in a different place.

The board is sold under the model name X99-MR9A, as well as E5-MR9A. Having one named the latter, I can confirm the motherboards are (almost?) identical and all the BIOSes etc. work on both.

## BIOS
The default BIOS is janky, to say the least - it does not provide support for some things that the motherboard handles on non-stock BIOS, such as sleep states or memory timings. It is hence recommended to flash a BIOS from a similar motherboard, in this case the Huananzhi X99-8M-F, as it works flawlessly on the MR9A. Attached to this repo are four BIOSes - a stock dump from the board, a Turbo Boost Unlocked + undervolted (-50mV) version sourced from Miyconst's [Mi899](https://github.com/miyconst/Mi899), a modified version with Resizable BAR capability added using Curi0's [ReBarUEFI](https://github.com/xCuri0/ReBarUEFI) (on top of TBU and undervolting), and, for shits and giggles, a version containing all the above alongside a modified boot splash logo (as I could not stand the "Huananzhi" logo, OCD moment). The BIOSes are labeled with a prefix. I recommend using FPT from inside Mi899 to flash the files. 

In case you encounter an error where FPT cannot gain access to sections of the BIOS, reboot to UEFI, manually turn BIOS protection (IntelRCSetup -> PCH Configuration -> Security Configuration -> BIOS Lock: Disable) on and off - EVEN if it is already disabled! - then save and reboot back to Windows for flashing.
