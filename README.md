# DVFW (Dolby Vision For Windows) Forked

Welcome to the DVFW GitHub repository by Team D4RK! This project aims to help users get Dolby Vision working on PCs. Contributions are welcome to improve and refine the process.


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

### Extra, FIX for 4K 144hz/165hz
1. Open CRU.
2. Select your display from the dropdown menu.
3. Go into Extension blocks and click Add...
4. Select Type: DisplayID 2.0 and click Add...
5. Select Detailed resolutions and click OK
6. Click Add... and select Timing: CVT-RB2 standard
7. Enter Active: 3840x2160 and Refresh rate 144.000 or 165.000 and click ALL OK button
8. Run Restart64.exe or Restart.exe found in the CRU folder to apply the changes.

## Screenshots

![App Screenshot](https://github.com/Team-D4RK/dolby-vision-for-windows/blob/main/app.png)
![Display Settings Screenshot](https://github.com/Team-D4RK/dolby-vision-for-windows/blob/main/displaysettings.png)

## Acknowledgements

- Special thanks to dogelitionhttps://linustechtips.com/topic/1145733-get-dolby-vision-instead-of-hdr10-on-windows-10/?do=findComment&comment=16314256for the initial guide.
- Special thanks to balu100 for the second guide.
