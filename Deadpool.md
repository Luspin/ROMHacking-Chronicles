**Deadpool**™ is a complete overhaul of the USA release of **Ninja Gaiden** for the NES, and can be downloaded from [ROMHacking.net](https://www.romhacking.net/hacks/4723/).

In this page, the author references an unknown version of the source ROM file, that I couldn't find anywhere:

|          | **CRC32**  | **SHA-1**                                  |
| -------- | ---------- | ------------------------------------------ |
| **File** | `11F953F6` | `CA513F841D75EFEB33BB8099FB02BEEB39F6BB9C` |
| **ROM**  | `7C4A72D8` | `15F245161179AB1959B7DC20E82ADD024D23AA3D` |

However, its isolated ROM signature did match a verified entry from the **[No-Intro](https://datomatic.no-intro.org/index.php?page=show_record&s=45&n=1569)** catalog:

|          | **CRC32**  | **SHA-1**                                  |
| -------- | ---------- | ------------------------------------------ |
| **File** | `80D3B95E` | `282C846DDBE968CC5E4D1ADC56DC9B8E3BEF4753` |
| **ROM**  | `7C4A72D8` | `15F245161179AB1959B7DC20E82ADD024D23AA3D` |

I concluded that the only differences between the two files were their iNES headers, and assumed the IPS file might overwrite them, so I applied the patch against a verified **No-Intro** ROM, but found serious graphical issues when loading the patched ROM file in the [Mesen2](https://github.com/SourMesen/Mesen2) emulator:

![Deadpool - No-Intro - Graphical Issues](Attachments/Screenshots/Deadpool%20-%20No-Intro%20-%20Graphical%20Issues.png)

After further investigation and a bit of trial-and-error, I found a different source ROM in the [NES Files](https://www.nesfiles.com/NES/Ninja_Gaiden/) page:

|          | **CRC32**  | **SHA-1**                                  |
| -------- | ---------- | ------------------------------------------ |
| **File** | `651DEC73` | `98162662B191BE485F307CE1D2BAE66F89DC15C0` |
| **ROM**  | `119964FF` | `42A3811E17870CD4F06502DE77B3564D424EFC15` |

This matched neither of the intended **File** or **ROM** signatures, but after applying the IPS file against it, I noticed an improvement in the graphical issues; although other issues were still present, e.g. the Deadpool sprite was corrupted:

![Deadpool - NES Files - Graphical Issues](Attachments/Screenshots/Deadpool%20-%20NES%20Files%20-%20Graphical%20Issues.png)

I then compared the iNES headers from the two **patched** ROM files:

|               |                                       |
| ------------- | ------------------------------------- |
| **No-Intro**  | `4e45531a 20204208 00000000 00000001` |
| **NES Files** | `4e45531a 20204200 00000061 73746572` |

After consulting with ChatGPT, I decided to modify the iNES headers of the patched **No-Intro** file:

|                             |                                       |
| --------------------------- | ------------------------------------- |
| **No-Intro (Header Fix 1)** | `4e45531a 20204200 00000061 73746572` |

**Success!** I finally had a fully working ROM file for **Deadpool**™:

![Deadpool - No-Intro (Header Fix 1)](Attachments/Screenshots/Deadpool%20-%20No-Intro%20(Header%20Fix%201).png)

ChatGPT also suggested further cleanup of the iNES headers:

|                             |                                       |
| --------------------------- | ------------------------------------- |
| **No-Intro (Header Fix 2)** | `4e45531a 20204200 0000000 000000000` |

This was confirmed to work flawlessly, so I generated a new IPS file - [Deadpool - No-Intro](Attachments/Files/Deadpool%20-%20No-Intro.ips)

It can be applied against a verified **No-Intro** source ROM file, through [Floating IPS](https://github.com/Alcaro/Flips) or [ROM Patcher JS](https://www.marcrobledo.com/RomPatcher.js/).

Lastly, **BIG** kudos to [Techmoon](https://www.romhacking.net/community/5543/) for all the work put into this ROM hack!