<div align="center">

# TomTom NAV4 — MSTMS Root, Map & Speedcam Update Guide
### Unlock Internal Storage & Install Latest Maps on TomTom NAV4 Devices (`Navcore 25.100`)

![Platform](https://img.shields.io/badge/Platform-TomTom%20NAV4%20Series-d40000?style=for-the-badge)
![Hardware Tested](https://img.shields.io/badge/Hardware%20Tested-GO%20500%20(Navcore%2025.100)-0078D7?style=for-the-badge)
![Verified Content](https://img.shields.io/badge/Verified-Iberia%201175.13264%20%2B%20Speedcams-2ea44f?style=for-the-badge)
![Author](https://img.shields.io/badge/By-IkerXD1437-ff6600?style=for-the-badge)

</div>

---

> [!IMPORTANT]
> **Compatibility & Hardware Testing Disclaimer:**
> This MSTMS + TTActivator workflow applies to the **TomTom NAV4 platform** (`GO 40/50/60`, `GO 500/510/600/610`, `GO 5000/5100/6000/6100`, `Start 40/50/60`, `Via 52/62`).
> It has been **physically tested and verified working on a TomTom GO 500 running Navcore `25.100.0001.311`** with map **`Iberia 1175.13264`** and updated Speedcams. While it has not been personally tested on other models, it should work identically across compatible NAV4 hardware.

---

## Download Mirrors

| Mirror | Host | Direct Link | Notes |
| :--- | :--- | :--- | :--- |
| **Mirror 1** | Internet Archive | **[Download from Archive.org](https://archive.org/details/tom-tom-nav-4-utilities-by-iker-xd-1437)** | Permanent preservation mirror |
| **Mirror 2** | MediaFire | **[Download from MediaFire](https://www.mediafire.com/file/uqqajs69s6ndcou/TomTom_NAV4_Utilities-By-IkerXD1437.zip/file)** | Fast permanent mirror |
| **Mirror 3** | Gofile | **[Download from Gofile](https://gofile.io/d/QAPp1aHX)** | High-speed direct mirror |

### File Verification (SHA-256)
* **Archive:** `TomTom_NAV4_Utilities-By-IkerXD1437.zip` *(199.4 MB — includes 10-language `README.txt`)*
```text
14b90ae8a7f216fdc3447574f0657753634d697e4fca880a2febd11818c58b1d
```

---

## What's Inside the Package

```text
TomTom_NAV4_Utilities-By-IkerXD1437/
├── MSTMS-Nav4-Navcore22.100-25.100/   # Main root & patching toolkit (Nav4Free.bat / .sh, FreeMyNav4.apk, TTInstall.Mini)
├── TTActivator-v1.22/                 # Map & Speedcam downloader/activator (Windows / Linux / macOS)
├── Install_All_ttpkg_nav4 (Extras)/   # [OPTIONAL EXTRAS] Batch .ttpkg installer & download_speedcam_1.7
├── meta.txt                           # Updated map activation key database
└── README.txt                         # Offline 10-language installation guide
```

### Detailed Folder Breakdown
* **`MSTMS-Nav4-Navcore22.100-25.100/`**: Contains **`Nav4Free.bat`** (Windows) and **`Nav4Free.sh`** (Linux/macOS), along with **`FreeMyNav4.apk`** (`files/`), **`TTInstall.Mini-20200829.exe`**, `windows/` ADB/LTools binaries, and `Executions/` (where full NAND backups are stored). Used to build the Magic SD card, back up the device, enable ADB/root, and patch the Navcore.
* **`TTActivator-v1.22/`**: Contains **`TTActivator.exe`** (v1.22 by *master131*) plus `.sh` / `.command` launchers and `meta.txt`. Used to download official `.ttpkg` maps/speedcams and push them over USB.
* **`meta.txt` (Root)**: Updated activation database ready to copy or push directly to the GPS via Option `5` in `Nav4Free.bat`.
* **`Install_All_ttpkg_nav4 (Extras)/`** *(Optional Extras)*: Contains **`download_speedcam_1.7.exe`**, **`Install_All_ttpkg_nav4.exe`**, and **`Install_Safety_Cam_SD_menu.bat`**.
  > [!NOTE]
  > **About the `(Extras)` folder:** These command-line batch utilities work by placing `.ttpkg` files in the same directory or dragging them onto the `.exe`. They are included **strictly as optional extras** (handy for batch-installing speedcams)—they were **not needed** for the main map installation, because installing the `.ttpkg` map directly from **TTActivator** after freeing internal storage in **Team MSTMS** worked cleanly without hanging on `"Triggering device..."`.

---

## Prerequisites & Critical Warnings

1. **Windows PC** with **`.NET Framework 4.8`** installed.
2. **TomTom `RNDIS` USB Drivers:** Install **MyDrive Connect** once on Windows so the network interface driver (`Remote NDIS Compatible Device`) is registered.
3. **Spare MicroSD Card + Working Card Reader:** Needed only temporarily for the **Magic SD** recovery boot (minimum **64 MB**). Make sure your SD adapter has an intact physical **Lock** switch—broken or missing Lock tabs force Windows into Read-Only mode (`Incorrect function` error).
4. **Data-Capable Micro-USB Cable:** Connect directly to a rear motherboard USB port.

> [!WARNING]
> **ALWAYS completely quit MyDrive Connect before running any tool!**
> Right-click the red TomTom icon in the Windows system tray (next to the clock) and select **Quit** (also verify no `MyDriveConnect` process remains in Task Manager). If MyDrive Connect is running in the background, it hijacks the USB/RNDIS port and causes connection timeouts.

> [!NOTE]
> **Windows Defender / Antivirus False Positives:** `TTActivator.exe` and `MSTMS` batch/patching binaries are frequently flagged as false positives. Add your extracted folder (e.g., `C:\TomTom_NAV4_Utilities-By-IkerXD1437`) to **Windows Security → Virus & threat protection → Manage settings → Exclusions** before running anything.

---

## Step-by-Step Installation Guide

### Phase 1 — Root & Patch the Device (`Nav4Free.bat`)

#### 1. Create the Magic SD Card
1. Insert a spare MicroSD card into your PC card reader.
2. Open `MSTMS-Nav4-Navcore22.100-25.100/` and run **`Nav4Free.bat`**.
3. Type **`1`** (`Create Magic sdcard`) and press **Enter**, following the on-screen drive selection prompt.
4. Safely eject the MicroSD card from Windows.

#### 2. Boot into Recovery Mode & Make a Full Backup
1. Insert the **Magic SD card** into your TomTom's MicroSD slot.
2. **Power off** the TomTom completely.
3. Press and **hold the Power button continuously** until the **black diagnostic screen with white system text** appears, then **quickly press the Power button 3 times**. The device will reboot and freeze on the **static TomTom logo** (Recovery Mode).
4. Connect the TomTom to your PC via USB.
   > [!CAUTION]
   > Windows will pop up multiple dialogs saying *"You need to format the disk in drive X: before you can use it"*. **Click Cancel / Ignore on ALL of them!** Formatting those raw Linux partitions will brick the device.
5. In **`Nav4Free.bat`**, type **`2`** (`Full Backup`) and press **Enter**. Wait until it completes (`Backup ended, stored in Executions/FullBackups/...`).

#### 3. Enable ADB & Root Shell
1. Keeping the TomTom in Recovery Mode with the Magic SD inserted, type **`3`** (`Enable ADB and root`) in **`Nav4Free.bat`** and press **Enter**.
2. Wait for confirmation: `Adb and root shell is now enabled on your device`.

#### 4. Install & Run `FreeMyNav4.apk`
1. Hold the TomTom Power button for **10–15 seconds** to reboot into **normal navigation mode**.
   *(Once patched, the GPS does not depend on the Magic SD card—you can remove or format it afterward).*
2. Verify **MyDrive Connect is closed**, reconnect the TomTom via USB in normal mode, and select **Option `4` (`Copy packages`)** in **`Nav4Free.bat`**.
3. The **Team MSTMS (`FreeMyNav4`)** interface will automatically launch on the TomTom touchscreen.
4. On the TomTom screen, tap **`Patch it`** and wait for confirmation (`Patching already done!`).
5. Tap **`Activate available content`** on the TomTom screen.

#### 5. Upload Updated `meta.txt`
1. Back in **`Nav4Free.bat`** on your PC, select **Option `5` (`Upload meta.txt to device`)**.
2. Wait for `meta.txt: 1 file pushed... Done!`.
3. Select **Option `8` (`Quit`)** to exit the script cleanly.

---

### Phase 2 — Free Up Internal Storage (Bypass "Not Enough Space")

> [!TIP]
> On NAV4 units, MyDrive Connect refuses to delete the factory map, and TTActivator's *"Delete internal memory maps"* button is often **grayed out**. You do **not** need manual `adb shell` commands to clear space—do it directly on the GPS touchscreen:

1. Open the **Team MSTMS (`FreeMyNav4`)** app on the TomTom touchscreen.
2. In the installed packages list, check the box for your **old factory map** *(e.g., `Europe 915.5053 (map, internal memory)`)* **AND its matching certificate** *(e.g., `DCT_Europe-xxx.meta (certificate, internal memory)`)*.
3. Tap **`Remove selected`** in the bottom-left corner.
4. Tap **`Back to main`**. You now have **5+ GB of free internal eMMC storage** ready for your updated map.

---

### Phase 3 — Download & Install Updated Maps (`TTActivator v1.22`)

1. Ensure **MyDrive Connect is completely closed** (check system tray).
2. Open **`TTActivator-v1.22/TTActivator.exe`**:
   * Go to the **Tools** tab and click **Update Meta.txt**.
   * Go to the **Map Downloader** tab.
   * Select generation: **`NAV4`**.
   * Choose your region *(e.g., **Iberia** ~500–900 MB, Southern Europe, or Europe)* and the latest version with a confirmed meta code *(verified: **`Iberia 1175.13264`**)*.
   * **CRITICAL:** **UNCHECK `Auto-Extract`**! If left checked, TTActivator unpacks raw files (`.dat`, `.sqlite`, `.meta`) and the `.ttpkg` installer will see an empty folder.
   * Click **Download to Folder** to save the clean `.ttpkg` package to your PC.
3. Switch to the **NAV3/NAV4 Tools** tab in TTActivator.
4. Click **`Install *.ttpkg files`**, select your downloaded `.ttpkg` map package, and wait for the transfer bar to reach **100%**.

#### Mandatory Drum-Roll Hard Reset (If Stuck on "Updating...")
Once the PC finishes at **100%**, the TomTom screen usually stays spinning indefinitely on **"Updating..."** because the installer does not send a session-close signal:
1. Verify no PC disk/transfer activity is still running, then **unplug the USB cable**.
2. Hold the TomTom Power button continuously for **20–30 seconds** until the screen turns off, lights back up, and plays the **TomTom drum-roll sound**, then release.
3. Once booted, open **Menu → Settings → Maps** (or *Switch Map*) and verify your updated map is active.

---

### Phase 4 — Install Updated Speedcams / Safety Cameras *(Optional)*

Map packages only include road speed limits—TomTom Speedcams are installed separately:

* **Method A (TTActivator):** Use the **TT Speedcam Downloader** tab inside `TTActivator.exe` to download and push speedcams over USB.
* **Method B (Batch Tool from `(Extras)`):**
  1. Ensure **MyDrive Connect** is closed.
  2. Open `Install_All_ttpkg_nav4 (Extras)/` and run **`download_speedcam_1.7.exe`** to download your region's `.ttpkg` speedcam files *(e.g., Spain/Iberia Premium)*.
  3. With the TomTom connected via USB, run **`Install_All_ttpkg_nav4.exe`** in the same folder.
  4. If the GPS stays on *"Updating..."* after 100%, unplug USB and perform a **20–30s drum-roll Hard Reset**.
  5. Enable alerts in **Menu → Settings → Sounds & Warnings → Speed Camera Warnings**.

---

## Technical Reference & Troubleshooting

| Parameter | Detail |
| :--- | :--- |
| **Target Architecture** | TomTom NAV4 (`RNDIS` virtual network interface, Linux eMMC partitions) |
| **Tested Hardware & OS** | TomTom GO 500 — Navcore `25.100.0001.311` |
| **Tested Map & Content** | `Iberia 1175.13264` + TomTom Safety Cameras |
| **Downgrade Support** | Not supported on NAV4 (anti-rollback bootloader blocks older Navcores) |
| **Magic SD Requirement** | Temporary only (used during Recovery Mode root/backup; not required afterward) |

| Issue | Cause | Fix |
| :--- | :--- | :--- |
| **No files appear when clicking `Install *.ttpkg`** | `Auto-Extract` was enabled in TTActivator | Uncheck **Auto-Extract** in Map Downloader and re-download so the file stays `.ttpkg`. |
| **"Not enough space" & delete button is grayed out** | Factory map fills internal memory; TTActivator blocks deletion | Delete the old map + its `DCT_*.meta` certificate directly inside the **Team MSTMS** app on the TomTom screen (Phase 2). |
| **Device not responding / connection error** | MyDrive Connect is hijacking the RNDIS port | Quit **MyDrive Connect** from the Windows system tray and Task Manager, then reconnect USB. |
| **TomTom stuck spinning on "Updating..."** | Normal NAV4 behavior after 100% `.ttpkg` transfer | Unplug USB and hold Power for **20–30s** until the **drum-roll** sound (Hard Reset). |
| **Windows Defender deletes `TTActivator.exe`** | Standard false positive on patching tools | Add the extracted folder to **Windows Security → Exclusions**. |
| **SD card gives `Incorrect function` in Windows** | Missing/broken side Lock tab on SD adapter | Swap to a healthy SD adapter or cover the left Lock notch with tape. |

---

<div align="center">
<sub>Compiled, documented, and hardware-tested on a <b>TomTom GO 500 (NAV4 — Navcore 25.100.0001.311)</b> by <b>IkerXD1437</b></sub>
</div>
