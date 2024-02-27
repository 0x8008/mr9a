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

**All the BIOS files supplied in this repo are only known to work with my motherboard. They might (and most likely will) work on your board, albeit proceed with caution. Anything you do is out of your own free will and was your decision - do not come to me crying if you fuck something up. I will not take any responsibility for your wrongdoing.**

The default BIOS is janky, to say the least - it does not provide support for some things that the motherboard handles on non-stock BIOS, such as sleep states or memory timings. It is hence recommended to flash a BIOS from a similar motherboard, in this case the Huananzhi X99-8M-F, as it works flawlessly on the MR9A. Attached to this repo are four BIOSes:
- a stock dump from the board,
- a Turbo Boost Unlocked + undervolted (-50mV) version sourced from Miyconst's [Mi899](https://github.com/miyconst/Mi899),
- a modified version with Resizable BAR capability added using Curi0's [ReBarUEFI](https://github.com/xCuri0/ReBarUEFI) (on top of TBU and undervolting),
- and, for shits and giggles, a version containing all the above alongside a modified boot splash logo (as I could not stand the "Huananzhi" logo, OCD moment). The BIOSes are labeled with a prefix. I recommend using FPT from inside Mi899 to flash the files. 

Remember to:
- restore default settings after flashing ANY of these BIOSes! Ignoring this step may result in issues.
- check if C6 states are turned OFF in C-states configuration (for any BIOS other than stock)

In case you encounter an error where FPT cannot gain access to sections of the BIOS, reboot to UEFI, manually turn BIOS protection (IntelRCSetup -> PCH Configuration -> Security Configuration -> BIOS Lock: Disable) on and off - EVEN if it is already disabled! - then save and reboot back to Windows for flashing.

## Drivers
Windows 10 installs most of the necessary drivers on its own, although there still is a lot of stuff missing in Device Manager. 

Before doing anything, I recommend replacing Windows' built in RTL8168/8111 driver, as it seems to cause weird networking issues (or at least it caused them for me on my particular board) with networking dropping out every now and again. The driver is present in this repo - file name sp137126.exe - the installer has HP branding, but it works fine on this board (it was the best .exe I could find, didn't want to drop the raw .inf/sys files).

The remaining devices don't seem to do much, although installing drivers would still likely be the perfect option (and it's what I do). Installing them is as easy as launching SDIO and letting it do the job; it can be downloaded using a torrent client (I recommend qBitTorrent) from [here](https://www.glenn.delahoy.com/downloads/sdio/SDIO_Update.torrent).

## Miscellaneous 

### Windows bootloader lost after flashing custom BIOS
Typical issue which also affects other Chinese boards. You can try fixing it (using the steps described [here](https://github.com/miyconst/Mi899/issues/45#issuecomment-872541322) by Miyconst), although most likely the fastest solution would be to simply reinstall Windows. 


