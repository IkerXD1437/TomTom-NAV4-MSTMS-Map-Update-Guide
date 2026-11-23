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

## Downloads (Releases)

All utility packages are available directly in the **[Releases](https://github.com/IkerXD1437/TomTom-NAV4-MSTMS-Map-Update-Guide/releases/latest)** section of this repository:

### Main Utilities & 10-Language Guide (`199.4 MB`)

| Package | Location | Notes |
| :--- | :--- | :--- |
| **`TomTom_NAV4_Utilities-By-IkerXD1437.zip`** | **[GitHub Releases](https://github.com/IkerXD1437/TomTom-NAV4-MSTMS-Map-Update-Guide/releases/latest)** | Full utility pack + offline 10-language `README.txt` |

#### File Verification (SHA-256)
- **Archive:** `TomTom_NAV4_Utilities-By-IkerXD1437.zip` *(includes 10-language `README.txt`)*
```text
14b90ae8a7f216fdc3447574f0657753634d697e4fca880a2febd11818c58b1d
```

### Community Speedcam Backup Pack (`3.5 MB`)

| Package | Location | Contents |
| :--- | :--- | :--- |
| **`17 22-10-2026.rar`** *(Europe Speedcams `22-10-2026`)* | **[GitHub Releases](https://github.com/IkerXD1437/TomTom-NAV4-MSTMS-Map-Update-Guide/releases/latest)** | 31 verified non-empty `.ttpkg` files (`ES`, `PT`, `FR`, `IT`, `DE`, `UK`, etc.) — courtesy of *papitchulo* |

---

## What's Inside the Package

```text
TomTom_NAV4_Utilities-By-IkerXD1437/
├── MSTMS-Nav4-Navcore22.100-25.100/   # Main root & patching toolkit (Nav4Free.bat / .sh, FreeMyNav4.apk, MSTMS_NAV4Free.img)
├── TTActivator-v1.22/                 # Map & Speedcam downloader/activator (Windows / Linux / macOS)
├── Install_All_ttpkg_nav4 (Extras)/   # [OPTIONAL EXTRAS] Batch .ttpkg installer & download_speedcam_1.7
├── meta.txt                           # Updated map activation key database
└── README.txt                         # Offline 10-language installation guide
```

### Detailed Folder Breakdown
- **`MSTMS-Nav4-Navcore22.100-25.100/`**: Contains **`Nav4Free.bat`** (Windows) and **`Nav4Free.sh`** (Linux/macOS), along with **`files/MSTMS_NAV4Free.img`** (Magic SD image), **`files/FreeMyNav4.apk`**, **`TTInstall.Mini-20200829.exe`**, `windows/` ADB/LTools binaries, and `Executions/` (where full NAND backups are stored).
- **`TTActivator-v1.22/`**: Contains **`TTActivator.exe`** (v1.22 by *master131*) plus `.sh` / `.command` launchers and `meta.txt`. Used to download official `.ttpkg` maps/speedcams and push them over USB.
- **`meta.txt` (Root)**: Updated activation database ready to copy or push directly to the GPS via Option `5` in `Nav4Free.bat`.
- **`Install_All_ttpkg_nav4 (Extras)/`** *(Optional Extras)*: Contains **`download_speedcam_1.7.exe`**, **`Install_All_ttpkg_nav4.exe`**, and **`Install_Safety_Cam_SD_menu.bat`**.

> [!NOTE]
> **About the `(Extras)` folder:** These command-line batch utilities work by placing `.ttpkg` files in the same directory or dragging them onto the `.exe`. They are included **strictly as optional extras** (handy for batch-installing speedcams)—they were **not needed** for the main map installation, because installing the `.ttpkg` map directly from **TTActivator** after freeing internal storage in **Team MSTMS** worked cleanly without hanging on `"Triggering device..."`.

---

## Prerequisites & Critical Warnings

1. **Windows PC** with **`.NET Framework 4.8`** installed.
2. **Rufus** *(recommended to flash the Magic SD in 3 seconds instead of waiting on `dd`)*.
3. **TomTom `RNDIS` USB Drivers:** Install **MyDrive Connect** once on Windows so the network interface driver (`Remote NDIS Compatible Device`) is registered.
4. **Spare MicroSD Card + Working Card Reader:** Needed only temporarily for the **Magic SD** recovery boot (minimum **64 MB**). Make sure your SD adapter has an intact physical **Lock** switch—broken or missing Lock tabs force Windows into Read-Only mode (`Incorrect function` error).
5. **Data-Capable Micro-USB Cable:** Connect directly to a rear motherboard USB port.

> [!WARNING]
> **ALWAYS completely quit MyDrive Connect before running any tool!**
> Right-click the red TomTom icon in the Windows system tray (next to the clock) and select **Quit** (also verify no `MyDriveConnect` process remains in Task Manager). If MyDrive Connect is running in the background, it hijacks the USB/RNDIS port and causes connection timeouts.

> [!NOTE]
> **Windows Defender / Antivirus False Positives:** `TTActivator.exe` and `MSTMS` batch/patching binaries are frequently flagged as false positives. Add your extracted folder (e.g., `C:\TomTom_NAV4_Utilities-By-IkerXD1437`) to **Windows Security → Virus & threat protection → Manage settings → Exclusions** before running anything.

---

## Step-by-Step Installation Guide

### Phase 1 — Root & Patch the Device

#### 1. Create the Magic SD Card *(Fast Method with Rufus — Recommended)*

> [!TIP]
> You *can* create the Magic SD using Option `1` in `Nav4Free.bat` (run as Administrator), but `dd` writes in 512-byte blocks on Windows and can take **30–60+ minutes** (~8 KB/s). Flashing `MSTMS_NAV4Free.img` directly with **Rufus** writes the exact same raw sectors in **~3 seconds**.

1. Insert a spare MicroSD card (all data on it will be erased) into your PC card reader.
2. Open **Rufus**, select your MicroSD under **Device**, and click **SELECT**.
3. Browse to `MSTMS-Nav4-Navcore22.100-25.100/files/` and select **`MSTMS_NAV4Free.img`** *(change the file filter to `All files (*.*)` if needed)*.
4. Click **START** and press **OK** on the warning confirming that all data on the SD card will be destroyed.
5. Wait a few seconds until the status bar turns green (**`READY`**), then click **CLOSE**.
6. If Windows pops up a dialog asking *"Format the disk in drive X: before you can use it"*, click **Cancel** (**NEVER format it**—the Magic SD uses Linux partitions), then safely eject the MicroSD.

| 1. Select `MSTMS_NAV4Free.img` in Rufus | 2. Click `OK` on Erase Warning |
| :---: | :---: |
| <img src="https://github.com/user-attachments/assets/72c205c7-b545-48d6-ac69-c692541d83a5" width="380" alt="Select MSTMS_NAV4Free.img in Rufus"> | <img src="https://github.com/user-attachments/assets/e7c0c862-2e21-4b6d-a12b-71f5fc5fa89a" width="320" alt="Confirm Erase Warning in Rufus"> |
| **3. Wait for `READY` & Click `CLOSE`** | **4. Click `Cancel` on Windows Format Popup** |
| <img src="https://github.com/user-attachments/assets/8a5d74ef-24ae-4d59-b2de-14ea5cb1fe8a" width="320" alt="Rufus Finished Ready"> | <img src="https://github.com/user-attachments/assets/87ac8fce-edd2-4b46-b2a9-e3f723e7cfd6" width="360" alt="Cancel Windows Format Prompt"> |

---

#### 2. Boot into Recovery Mode & Make a Full Backup (`Nav4Free.bat` — Option `2`)

> [!IMPORTANT]
> **Run `Nav4Free.bat` as Administrator!** Right-click `MSTMS-Nav4-Navcore22.100-25.100/Nav4Free.bat` → **Run as administrator** to prevent `dd: Permission denied` errors.
> Notice how the script detects your TomTom: it first asks you to **DISCONNECT** the device (type `y` + Enter so it scans existing drives), and then tells you to **CONNECT** it (type `y` + Enter so it detects the new drive).

1. Insert the **Magic SD card** into your TomTom's MicroSD slot.
2. **Power off** the TomTom completely.
3. Press and **hold the Power button continuously** until the **black diagnostic screen with white system text** appears, then release and **quickly press the Power button 3 times**. The device will reboot and freeze on the **static TomTom logo** (Recovery Mode).

https://github.com/user-attachments/assets/2d8c2d7c-b6a7-401f-ab3d-9bb58824bd87

4. Launch **`Nav4Free.bat`** as Administrator, type **`2`** (`Create device full backup`) and press **Enter**.
5. When asked `Is the device now DISCONNECTED ? (y/n)?`, keep the TomTom unplugged, type **`y`** and press **Enter**.
6. Now **connect the TomTom** (in Recovery Mode) to your PC via USB.

> [!CAUTION]
> Windows will pop up multiple dialogs saying *"You need to format the disk in drive X: before you can use it"*. **Click Cancel / Ignore on ALL of them!** Formatting those raw Linux partitions will permanently damage the device.

7. When asked `Is the device now CONNECTED (y/n)?`, type **`y`** and press **Enter**. Wait for the full backup to finish (`Backup ended, stored in Executions/FullBackups/...`).

<div align="center">
  <img src="https://github.com/user-attachments/assets/e6c95e6f-8ab8-4400-a3b4-1b84a5aa9d67" width="680" alt="Nav4Free Option 2 Create Full Backup">
</div>

---

#### 3. Enable ADB & Root Shell (`Nav4Free.bat` — Option `3`)
1. Keeping the TomTom in **Recovery Mode** with the Magic SD inserted, type **`3`** (`Enable ADB and root`) in **`Nav4Free.bat`** and press **Enter**.
2. Follow the same disconnect (`y`) → connect (`y`) prompt if requested (canceling any Windows format popups again).
3. Wait for confirmation: `Adb and root shell is now enabled on your device` and `Reboot the device in normal mode`.

<div align="center">
  <img src="https://github.com/user-attachments/assets/0e1ed671-e0b2-482f-bf07-5fa6527c009e" width="680" alt="Nav4Free Option 3 Enable ADB and Root">
</div>

---

#### 4. Copy Packages & Run `FreeMyNav4.apk` (`Nav4Free.bat` — Option `4`)
1. Hold the TomTom Power button for **10–15 seconds** to reboot into **normal navigation mode**.
   *(Once patched, the GPS does not depend on the Magic SD card—you can remove or reuse it afterward).*
2. Verify **MyDrive Connect is closed**, reconnect the TomTom via USB in **normal mode**, and type **`4`** (`Copy packages`) in **`Nav4Free.bat`**.
3. Wait for the script to push the files and launch **`FreeMyNav4.apk`** automatically on the TomTom touchscreen.

<div align="center">
  <img src="https://github.com/user-attachments/assets/d22bb522-febf-4f57-972d-54575324a751" width="680" alt="Nav4Free Option 4 Copy Packages">
</div>

4. On the TomTom screen (**Team MSTMS / `Free my NAV4!`**), tap **`Patch it`** and wait for confirmation (`Patching already done!`).
5. Tap **`Activate available content`** on the TomTom screen.

| 1. Team MSTMS Boot Screen | 2. `Free my NAV4!` — Patch & Activate |
| :---: | :---: |
| <img src="https://github.com/user-attachments/assets/c6ed16b8-167a-4ecb-a886-2681adff4e1d" width="380" alt="Team MSTMS Splash Screen"> | <img src="https://github.com/user-attachments/assets/9077cd96-3589-41d8-ab24-164753cc79b4" width="380" alt="Free my NAV4 Patch and Activate"> |

---

#### 5. Upload Updated `meta.txt` & Quit (`Nav4Free.bat` — Options `5` & `8`)
1. Back in **`Nav4Free.bat`** on your PC, type **`5`** (`Upload meta.txt to device`) and press **Enter**.
2. Wait for `meta.txt: 1 file pushed... Done!`.
3. Type **`8`** (`Quit`) to exit the script cleanly.

<div align="center">
  <img src="https://github.com/user-attachments/assets/cab89c48-5e09-4712-aa24-cb2bf91914e5" width="680" alt="Nav4Free Option 5 Upload meta.txt and Quit">
</div>

---

### Phase 2 — Free Up Internal Storage (Bypass "Not Enough Space")

> [!TIP]
> On NAV4 units, MyDrive Connect refuses to delete the factory map, and TTActivator's *"Delete internal memory maps"* button is often **grayed out**. You do **not** need manual `adb shell` commands to clear space—do it directly on the GPS touchscreen:

1. Open the **Team MSTMS (`FreeMyNav4`)** package manager on the TomTom touchscreen.
2. In the installed packages list, check the box for your **old factory map** *(e.g., `Europe 915.5053 (map, internal memory)`)* **AND its matching certificate** *(e.g., `DCT_Europe-xxx.meta (certificate, internal memory)`)*.
3. Tap **`Remove selected`** in the bottom-left corner.
4. Tap **`Back to main`**. You now have **5+ GB of free internal eMMC storage** ready for your updated map.

<div align="center">
  <img src="https://github.com/user-attachments/assets/d673ddc7-d4bc-40e9-9755-f5232fca0e81" width="460" alt="Team MSTMS Package Manager on TomTom Screen">
</div>

---

### Phase 3 — Download & Install Updated Maps (`TTActivator v1.22`)

1. Ensure **MyDrive Connect is completely closed** (check system tray).
2. Open **`TTActivator-v1.22/TTActivator.exe`**:
   - Go to the **Tools** tab and click **Update Meta.txt**.
   - Go to the **Map Downloader** tab.
   - Select generation: **`nav4`**.
   - Choose your region *(e.g., **Iberia** ~500–1000 MB, Southern Europe, or Europe)* and the latest version with a confirmed meta code *(verified: **`Iberia 1175.13264`**)*.
   - **CRITICAL:** **UNCHECK `Auto-Extract`** and confirm **Yes** on the popup! If left checked, TTActivator unpacks raw files (`.dat`, `.sqlite`, `.meta`) and the `.ttpkg` installer will see an empty folder.
   - Click **Download To Folder** to save the clean `.ttpkg` package (`Iberia_1175_13264_tmp_0.ttpkg`) to your PC.

| 1. Uncheck `Auto-Extract` (`nav4` / `1175`) | 2. Clean `.ttpkg` Package Downloaded |
| :---: | :---: |
| <img src="https://github.com/user-attachments/assets/567d3a9c-05e9-41db-a400-0c2e62efcf0c" width="380" alt="TTActivator Disable Auto-Extract"> | <img src="https://github.com/user-attachments/assets/c2023c3e-4fee-4cd7-9cbf-9edb2f1acf63" width="380" alt="TTActivator Map Downloaded as .ttpkg"> |

3. Switch to the **NAV3/NAV4 Tools** tab in TTActivator.
4. Click **`Install TT Package Files`**, select your downloaded `.ttpkg` map package, and wait for the transfer bar to reach **100%**.

<div align="center">
  <img src="https://github.com/user-attachments/assets/64eb8845-0b71-42a3-acb1-e5f4c18a4d82" width="520" alt="TTActivator Install TT Package Files">
</div>

#### Mandatory Drum-Roll Hard Reset (If Stuck on "Updating...")
Once the PC finishes at **100%**, the TomTom screen usually stays spinning indefinitely on **"Updating..."** because the installer does not send a session-close signal:
1. Verify no PC disk/transfer activity is still running, then **unplug the USB cable**.
2. Hold the TomTom Power button continuously for **20–30 seconds** until the screen turns off, lights back up, and plays the **TomTom drum-roll sound**, then release.
3. Once booted, open **Menu → Settings → Maps** (or *Switch Map*) and verify your updated map is active.

---

### Phase 4 — Install Updated Speedcams / Safety Cameras *(Optional)*

Map packages only include road speed limits—TomTom Speedcams are installed separately as `.ttpkg` files:

- **Method A (TTActivator Live Download):** Use the **Safety Cam Downloader** tab inside `TTActivator.exe` to download and push speedcams over USB.
- **Method B (Community Offline Speedcam Pack — Recommended if TomTom servers return empty `0 KB` files):**
  1. Download **`17 22-10-2026.rar`** from **[GitHub Releases](https://github.com/IkerXD1437/TomTom-NAV4-MSTMS-Map-Update-Guide/releases/latest)** and extract it (contains 31 European country `.ttpkg` packages such as `safety-cam-es-premium-22-10-2026.ttpkg`, `safety-cam-pt-premium-22-10-2026.ttpkg`, `safety-cam-fr-premium-22-10-2026.ttpkg`, etc.).
  2. With **MyDrive Connect** closed and the TomTom connected via USB, either:
     - Open **TTActivator → NAV3/NAV4 Tools → `Install TT Package Files`** and select only the country `.ttpkg` files you need, **OR**
     - Place the desired `.ttpkg` files in the same folder as **`Install_All_ttpkg_nav4.exe`** (`Install_All_ttpkg_nav4 (Extras)/`) and run it to batch-install all of them at once.
- **Method C (`download_speedcam_1.7.exe` from `(Extras)`):**
  1. Ensure **MyDrive Connect** is closed.
  2. Open `Install_All_ttpkg_nav4 (Extras)/` and run **`download_speedcam_1.7.exe`** to download your region's `.ttpkg` speedcam files, then run **`Install_All_ttpkg_nav4.exe`** in the same folder.

> [!NOTE]
> **TomTom Speedcam Server Outages (Empty `0 KB` Files):** TomTom's official speedcam servers intermittently fail and return empty (`0 KB`) `.ttpkg` files on certain days in both **TTActivator** and **`download_speedcam_1.7.exe`**. If a region downloads empty, use **Method B** above from **[GitHub Releases](https://github.com/IkerXD1437/TomTom-NAV4-MSTMS-Map-Update-Guide/releases/latest)**.

- After installing speedcams, if the GPS stays spinning on *"Updating..."* after 100%, unplug USB and perform a **20–30s drum-roll Hard Reset**.
- Enable alerts in **Menu → Settings → Sounds & Warnings → Speed Camera Warnings**.

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
| **`dd: Permission denied` or extremely slow Magic SD write (~8 KB/s)** | `Nav4Free.bat` not run as Admin, or `dd` using tiny 512-byte blocks | Run `Nav4Free.bat` **as Administrator**, or flash `files/MSTMS_NAV4Free.img` directly with **Rufus** (~3 seconds). |
| **No files appear when clicking `Install TT Package Files`** | `Auto-Extract` was enabled in TTActivator | Uncheck **Auto-Extract** in Map Downloader and re-download so the file stays `.ttpkg`. |
| **"Not enough space" & delete button is grayed out** | Factory map fills internal memory; TTActivator blocks deletion | Delete the old map + its `DCT_*.meta` certificate directly inside the **Team MSTMS** app on the TomTom screen (Phase 2). |
| **Speedcam `.ttpkg` downloads empty (`0 KB`)** | Intermittent TomTom speedcam server outage | Download the offline **Community Europe Speedcam Pack (`17 22-10-2026.rar`)** from **[GitHub Releases](https://github.com/IkerXD1437/TomTom-NAV4-MSTMS-Map-Update-Guide/releases/latest)**. |
| **Device not responding / connection error** | MyDrive Connect is hijacking the RNDIS port | Quit **MyDrive Connect** from the Windows system tray and Task Manager, then reconnect USB. |
| **TomTom stuck spinning on "Updating..."** | Normal NAV4 behavior after 100% `.ttpkg` transfer | Unplug USB and hold Power for **20–30s** until the **drum-roll** sound (Hard Reset). |
| **Windows Defender deletes `TTActivator.exe`** | Standard false positive on patching tools | Add the extracted folder to **Windows Security → Exclusions**. |
| **SD card gives `Incorrect function` in Windows** | Missing/broken side Lock tab on SD adapter | Swap to a healthy SD adapter or cover the left Lock notch with tape. |

---

<div align="center">
<sub>Compiled, documented, and hardware-tested on a <b>TomTom GO 500 (NAV4 — Navcore 25.100.0001.311)</b> by <b>IkerXD1437</b></sub>
</div>
