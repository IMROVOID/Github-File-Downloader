# Universal File Downloader Action

A powerful GitHub Actions workflow that downloads any file from the web directly into your repository. It automatically organizes, compresses, and splits large files, generates detailed readme files, and supports password-protected archives—all with zero local setup.

> **Base project:** This workflow is heavily inspired by and builds upon the ideas from [UDL-3](https://github.com/nikzad-avasam/UDL-3/). Many thanks to the original authors for their pioneering work!

## ✨ Key Features

### General & Core Capabilities
- **🌐 Universal Downloading:** Download any file from any direct URL. Supports single and batch downloads (multiple URLs separated by space).
- **🔄 Robust Download Engine:** Combines `aria2` (for high-speed, multi-connection transfers) and `curl` (as a fallback) with intelligent retry logic to handle unstable connections.
- **📦 Archive or Plain Storage:** Choose between `normal` mode (files saved as‑is) or `zip` mode (compressed into a single 7z archive).
- **🔐 Optional Encryption:** Protect your archives with a password. The password is embedded in the generated README so you never lose it.
- **📏 Configurable Splitting:** Split large archives into smaller parts (10–90 MB) to bypass upload size limits or make sharing easier.
- **⚙️ Adaptive Compression:** Choose a preset (`auto`, `best`, `great`, `good`, `fast`, `fastest`); the `auto` mode intelligently picks the highest compression level that can finish within the action’s time limit.
- **📂 Incremental Git Push:** Files are committed and pushed in small batches to avoid timeout errors, even with repositories weighing tens of gigabytes.

### Special & Unique Features
- **🕒 Timestamped Organization:** Every run creates a uniquely named folder like `download_20260514_140437` or `archive_20260514_140437`. No more overwritten files.
- **📋 Auto‑Generated READMEs:** Each download folder/archive automatically gets a comprehensive `README.md` that includes:
  - List of all files with their sizes
  - Job execution start time
  - Compression level and number of parts (if archived)
  - Contents of the 7z archive (so you know exactly what’s inside without downloading)
- **🏗️ Stair‑Format Tree Listing:** The main `downloads/README.md` shows a tree view of each folder’s contents (first 5 items) along with size, part count, and timestamp—perfect for quick browsing.
- **📎 One‑Click Copy All Links:** Every README includes a “Download Manager” block containing all part links, ready to be copied and pasted into tools like JDownloader.
- **🏋️ Heavy File Handling:** Tested with files up to 28 GB, and capable of handling downloads above 50 GB thanks to smart batching and resume‑friendly transport.
- **🧠 Smart Archive Naming:** In `zip` mode, if only one file is downloaded, the archive takes its name (shortened if it’s too long) instead of a generic name—keeping things human‑readable.

## 📁 Project Structure

```
.
├── .github
│   └── workflows
│       └── download.yml          # Main workflow definition
├── downloads                     # (Created after first run) All downloaded content
├── README.md                     # This file
└── LICENSE                       # GNU GPL v3.0
```

The entire logic resides in a single workflow file. No external build steps or dependencies—just fork, configure, and run.

## ⚙️ How to Use

1. **Fork the repository** to your own GitHub account.
2. Go to the **Actions** tab in your fork.
3. Select the **⬇️ 01- Download URL** workflow on the left.
4. Click **“Run workflow”** and fill in the inputs:
   - **URLs:** The download link(s), separated by spaces.
   - **Mode:** `normal` (store files as‑is) or `zip` (compress into a 7z archive).
   - **Part size:** Split archive part size in MB (10–90, default 45).
   - **Password:** (Optional) Password to encrypt the archive.
   - **Compression Preset:** Choose a compression level (auto recommended).
5. Click **“Run workflow”** and wait for the action to complete.
6. After completion, your files will appear in the `downloads/` folder, organised by timestamp and accompanied by a detailed `README.md`.

## 🔧 How to Modify

The entire behaviour is controlled by the YAML file located at `.github/workflows/download.yml`. You can edit it directly in your fork to change:

- Default split size or compression level.
- Maximum download time (`timeout-minutes`).
- Git push batching parameters.
- The naming conventions for folders and archives.
- The contents of the auto‑generated README files.

Just open the file in GitHub’s editor, make your changes, and commit. The next run will use your custom settings.

## 🛠️ Technologies & Libraries Used

| Library / Tool | Description |
| :--- | :--- |
| **GitHub Actions** | Hosts and orchestrates the entire workflow. |
| **aria2** | Lightweight multi‑connection download utility. |
| **p7zip‑full** | Command‑line version of 7‑Zip, providing LZMA2 compression and splitting. |
| **curl** | Transfers data from URLs, used as a fallback downloader. |
| **bc** | Arbitrary precision calculator for estimating compression times. |
| **Python 3** | Used for URL‑encoding helper functions. |

## 🙏 Credits

This project started from the excellent work of the [UDL-3](https://github.com/nikzad-avasam/UDL-3/) repository. The foundation, inspiration, and many core ideas came from there. Huge thanks to the original authors!

## 📜 License

This project is open-source and licensed under the **[GNU General Public License v3.0 (GPL-3.0)](https://choosealicense.com/licenses/gpl-3.0/)**.

### Summary of Key Requirements

The GPL-3.0 is a strong copyleft license that ensures the software remains free. If you use, modify, or distribute this code, you must adhere to the following:

* **Disclose Source:** You must make the source code available when you distribute the software.
* **License & Copyright Notice:** You must include a copy of the license and the original author's copyright notice.
* **Same License (Copyleft):** Any modifications or derived works must also be licensed under GPL-3.0.
* **State Changes:** You must clearly indicate if you have modified the original files.
* **No Warranty:** This software is provided "as is" without any warranty of any kind.

> This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
>
> This program is distributed in the hope that it will be useful, but **WITHOUT ANY WARRANTY**; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

For full details, please refer to the [LICENSE](/LICENSE) file in this repository.

---

## © About the Developer

I'm a passionate professional specializing in Graphic Design, Web Development, and cross-platform app development with Dart & Flutter. I thrive on turning innovative ideas into reality, whether it's a stunning visual, a responsive website, or a polished desktop app like this one. I also develop immersive games using Unreal Engine.

* **Website:** [rovoid.ir](https://rovoid.ir)
* **GitHub:** [IMROVOID](https://github.com/IMROVOID)
* **LinkedIn:** [Roham Andarzgou](https://www.linkedin.com/in/roham-andarzgouu)

### 🙏 Support This Project

If you find this application useful, please consider a donation. As I am based in Iran, cryptocurrency is the only way I can receive support. Thank you!

| Cryptocurrency | Address |
| :--- | :--- |
| **Bitcoin** (BTC) | `bc1qd35yqx3xt28dy6fd87xzd62cj7ch35p68ep3p8` |
| **Ethereum** (ETH) | `0xA39Dfd80309e881cF1464dDb00cF0a17bF0322e3` |
| **USDT** (TRC20) | `THMe6FdXkA2Pw45yKaXBHRnkX3fjyKCzfy` |
| **Solana** (SOL) | `9QZHMTN4Pu6BCxiN2yABEcR3P4sXtBjkog9GXNxWbav1` |
| **TON** | `UQCp0OawnofpZTNZk-69wlqIx_wQpzKBgDpxY2JK5iynh3mC` |
