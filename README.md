# DVFW (Dolby Vision For Windows) - Forked by Team D4RK

Welcome to the DVFW GitHub repository by Team D4RK! This project aims to help users get Dolby Vision working on PCs. 


## Current Best Known Guide

Follow these steps to enable Dolby Vision on your PC:

### Prerequisites
1. [Dolby Access](https://apps.microsoft.com/detail/9n0866fs04w8?hl=en-US&gl=US)
2. [Dolby Vision Extensions](https://www.microsoft.com/en-gb/p/dolby-vision-extensions/9pltg1lwphlf)
3. [HEVC Video Extensions](https://apps.microsoft.com/detail/9NMZLZ57R3T7?hl=en-US&gl=US)
4. [CRU](https://www.monitortests.com/forum/Thread-Custom-Resolution-Utility-CRU)
5. [AW EDID Editor](https://www.analogway.com/emea/products/software-tools/aw-edid-editor/)

### Steps
1. Download and install all prerequisites.
2. Open CRU.
3. Select your display from the dropdown menu.
4. Export the current EDID to a file (e.g., dolbyvisionmonitor.bin).
5. Download AW EDID Editor.
6. Open AW EDID Editor.
7. Open the exported EDID file (dolbyvisionmonitor.bin).
8. Under CEA Extension, navigate to the Vendor-Specific Video section with a matching "IEEE OUI" of 53318, this is the Dolby OUI.

 - if you can't find a Vendor-Specific Video section with a matching IEEE OUI value, it may be the case that your display does not support Dolby Vision

9. Copy the Payload (HEX String).
10. Go here https://dvfw.netlify.app/ and paste your Payload (HEX String).
11. Click on Decode and click Enable Dolby Vision Mode (Enable LLDV-HDMI (v2) or other (Check Action Output Section))
12. Return in AW EDID Editor and paste the new Payload (HEX String) and save edited EDID file (e.g., fixeddolbyvisionmonitor.bin)
12. Return in CRU again and Import the edited EDID file (fixeddolbyvisionmonitor.bin).
13. Run Restart64.exe or Restart.exe found in the CRU folder to apply the changes.

## FIX for 4K 144hz/165hz
1. Open CRU.
2. Select your display from the dropdown menu.
3. Go into Extension blocks and click Add...
4. Select Type: DisplayID 2.0 and click Add...
5. Select Detailed resolutions and click OK
6. Click Add... and select Timing: CVT-RB2 standard
7. Enter Active: 3840x2160 and Refresh rate 144.000 or 165.000 and click ALL OK button
8. Run Restart64.exe or Restart.exe found in the CRU folder to apply the changes.

## FIX for NITS limit
### 1. Change nits limit
1. Open CRU.
2. Select your display from the dropdown menu.
3. Go into Extension blocks and edit CTA-861
4. In Data blocks edit HDR static metadata
5. Under HDR static metadata. Change value for Max luminance and Max frame-avg
-  (Put your real Screen NITS limit for this check bellow Step 2 (HDR calibration))
6. After change. Click ALL OK button and Run Restart64.exe or Restart.exe found in the CRU folder to apply the changes.

### 2. Calibrate Using the Windows HDR Calibration App
After applying your target value in CRU and running `restart64.exe` to refresh your graphics drivers:

1. Launch the official **Windows HDR Calibration** app (available for free on the Microsoft Store).
2. Follow the on-screen instructions until you reach the white pattern test screens.
3. Adjust the sliders until the textured pattern disappears completely. 
4. The pattern should become invisible exactly when the app's digital readout matches your display's target nits value (e.g., 800, 1000, 5000, etc.).

| Luminosité cible (Nits) | Valeur exacte CRU (Code Value) | Équivalent réel calculé | Type d'écran courant |
| :--- | :--- | :--- | :--- |
| **400 nits** | **96** | 400 nits | Écrans PC entrée de gamme (HDR 400) |
| **600 nits** | **115** | 603 nits | Moniteurs IPS/VA certifiés HDR 600 |
| **800 nits** | **128** | 800 nits | Écrans OLED classiques (LG C1/C2/C3, ASUS, MSI) |
| **1 000 nits** | **139** | 1 015 nits | OLED récents (QD-OLED Gen 3, LG G4) / Mini-LED |
| **1 300 nits** | **151** | 1 310 nits | Écrans OLED haut de gamme (mode Peak Highlighter) |
| **1 500 nits** | **157** | 1 542 nits | TV Mini-LED intermédiaires (Samsung QN90, Sony) |
| **2 000 nits** | **170** | 2 000 nits | TV Mini-LED très lumineuses (TCL C805/C845) |
| **3 000 nits** | **193** | 3 044 nits | TV Mini-LED Premium (Samsung QN95, Hisense U8) |
| **4 000 nits** | **205** | 4 063 nits | Écrans de référence de mastering (Dolby Vision) |
| **5 000 nits** | **213** | 5 042 nits | TV Extrêmes (Hisense 75U88QG, TCL X955) |

## Screenshots

![App Screenshot](https://github.com/Team-D4RK/dolby-vision-for-windows/blob/main/app.png)
![Display Settings Screenshot](https://github.com/Team-D4RK/dolby-vision-for-windows/blob/main/displaysettings.png)

## Acknowledgements

- Special thanks to dogelition for the first guide

  
- Special thanks to balu100 for the second guide.
