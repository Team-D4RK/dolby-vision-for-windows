# DVFW (Dolby Vision For Windows) - Forked by Team D4RK

Welcome to the DVFW GitHub repository by Team D4RK! This project aims to help users successfully enable Dolby Vision on Windows PCs.

---

## Current Best Known Guide

Follow these steps to enable Dolby Vision on your PC:

### Prerequisites
1. [Dolby Access](https://apps.microsoft.com/detail/9n0866fs04w8?hl=en-US&gl=US)
2. [Dolby Vision Extensions](https://www.microsoft.com/en-gb/p/dolby-vision-extensions/9pltg1lwphlf)
3. [HEVC Video Extensions](https://apps.microsoft.com/detail/9NMZLZ57R3T7?hl=en-US&gl=US)
4. [CRU (Custom Resolution Utility)](https://www.monitortests.com/forum/Thread-Custom-Resolution-Utility-CRU)
5. [AW EDID Editor](https://www.analogway.com/emea/products/software-tools/aw-edid-editor/)

### Step 1 - Dolby Vision Certification
1. Download and install all prerequisites listed above.
2. Open `CRU.exe`.
3. Select your active display from the top dropdown menu.
4. Export the current EDID to a file (e.g., `dolbyvisionmonitor.bin`).
5. Open `AW EDID Editor`.
6. Load your exported file (`dolbyvisionmonitor.bin`).
7. Under the **CEA Extension** tab, navigate to the **Vendor-Specific Video** section and locate the entry with a matching "IEEE OUI" of `53318` (this is the Dolby OUI).
   * *Note: If you cannot find a Vendor-Specific Video section with this exact IEEE OUI value, your display might not natively support Dolby Vision.*
8. Copy the Payload (HEX String).
9. Go to [dvfw.netlify.app](https://dvfw.netlify.app/) and paste your Payload (HEX String).
10. Click on **Decode** and then **Enable Dolby Vision Mode** (Select *Enable LLDV-HDMI (v2)* or other recommended profile based on the *Action Output Section*).
11. Return to `AW EDID Editor`, paste the newly generated Payload (HEX String), and save the edited EDID file (e.g., `fixeddolbyvisionmonitor.bin`).
12. Go back to `CRU.exe` and click **Import** to load your edited file (`fixeddolbyvisionmonitor.bin`).
13. Run `restart64.exe` (or `restart.exe`) from the CRU folder to refresh your graphics drivers.

### Step 2 - Enable Dolby Vision in Windows Settings
1. Right-click on your desktop and select **Display settings**.
2. Scroll down and enter the **HDR** section.
3. Toggle **Use HDR** to **On**.
4. Check the box to activate **Dolby Vision mode** if prompted, or verify that the active color space profile is properly engaged.

---

## FIX for 4K 144Hz / 165Hz
If your display supports high refresh rates but gets limited after modifying the EDID, follow these steps:
1. Open `CRU.exe`.
2. Select your active display from the dropdown menu.
3. Under **Extension blocks**, click **Add...**
4. Select **Type: DisplayID 2.0** and click **Add...**
5. Select **Detailed resolutions** and click **OK**.
6. Click **Add...** and select **Timing: CVT-RB2 standard**.
7. Set **Active resolution** to `3840x2160` and enter your native refresh rate (`144.000` or `165.000`).
8. Click **OK** on all subsequent windows to save, then run `restart64.exe` to apply changes.

---

## FIX for NITS Limit

### 1. Adjusting the Hardware Nits Cap in CRU
By default, Windows may misread your screen's true peak brightness. You can override this using CRU:
1. Open `CRU.exe` and select your active display.
2. Go into **Extension blocks** and double-click **CTA-861**.
3. In the **Data blocks** list, double-click **HDR static metadata**.
4. Modify the values for **Max luminance** and **Max frame-avg** using the Code Values (CV) table below corresponding to your screen's real peak hardware capability.
5. Click **OK** on all windows and run `restart64.exe`. Finally, **fully restart your PC** to force Windows to reload the display profile.

### 2. Calibrating with the Windows HDR Calibration App
Once your PC has rebooted, you need to sync the OS tone curve using the official calibration tool:

1. Launch the **Windows HDR Calibration** app (free on the Microsoft Store).
2. Follow the on-screen instructions until you reach the **Minimum Luminance (Blacks)** test screen.
3. **For Minimum Luminance:** Adjust the slider until the pattern barely disappears. 
   * *Note: OLEDs will usually disappear at **0**. High-end ADS Pro / IPS panels (like the Hisense U88QG) will naturally disappear around **1350** (1.35 nits) due to subtle backlight bleeding. Trust your eyes.*
4. **For Maximum Luminance & Full-Frame Luminance:** Adjust the sliders until the textured pattern disappears completely. 
   * *⚠️ Hardware Limitation Bug:* On extremely bright displays (4000+ nits), the Windows UI slider might lock itself and refuse to go past a specific limit (e.g., **2800 nits**). If this happens, simply **drag the slider all the way to the right to max it out at 2800**. Windows will push its widest signal, and your display's internal hardware processor will handle the rest flawlessly.

### CRU Nits Conversion Table (CTA-861 Standard)
Use these exact Code Values inside CRU to map your target nits:


| Target Brightness (Nits) | Exact CRU Code Value | Calculated Real Equivalent | Common Display Type |
| :--- | :--- | :--- | :--- |
| **400 nits** | **96** | 400 nits | Entry-level PC monitors (HDR 400) |
| **600 nits** | **115** | 603 nits | Mid-range IPS/VA monitors (HDR 600) |
| **800 nits** | **128** | 800 nits | Standard OLED displays (LG C1/C2/C3, ASUS, MSI) |
| **1,000 nits** | **139** | 1,015 nits | Modern OLEDs (QD-OLED Gen 3, LG G4) / Mini-LED |
| **1,300 nits** | **151** | 1,310 nits | Premium OLEDs (Peak Highlighter modes) |
| **1,500 nits** | **157** | 1,542 nits | Mid-tier Mini-LED TVs (Samsung QN90, Sony) |
| **2,000 nits** | **170** | 2,000 nits | High-brightness Mini-LED TVs (TCL C845) |
| **3,000 nits** | **193** | 3,044 nits | Premium Mini-LED TVs (Samsung QN95) |
| **4,000 nits** | **205** | 4,063 nits | Mastering Reference Monitors |
| **5,000 nits** | **213** | 5,042 nits | Extreme Mini-LED displays (Hisense U88QG, TCL X955) |

### ℹ️ Note on the "10,000 nits" Value in Windows Advanced Settings
If your Windows Advanced Display settings show a peak brightness of **10,000 nits** alongside a **Dolby Vision Certification**, your setup is working perfectly! 

This is intended behavior because Dolby Vision entirely bypasses standard Windows software restrictions. Windows is simply displaying the maximum container protocol ceiling of Dolby Vision. Rest assured, your TV's hardware processor will automatically track and map the incoming signal up to its true maximum hardware capability (e.g., 5,000 nits) without clipping any specular highlights.

---

## Screenshots

![App Screenshot](https://github.com/Team-D4RK/dolby-vision-for-windows/blob/main/app.png)
![Display Settings Screenshot](https://github.com/Team-D4RK/dolby-vision-for-windows/blob/main/displaysettings.png)

## Acknowledgements

- Special thanks to **dogelition** for the first guide.
- Special thanks to **balu100** for the second guide.
