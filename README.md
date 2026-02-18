# 📚 ACSM to Kindle Converter

**Pure Python DRM Removal Tool for Personal EPUB Library Management**

Remove Adobe DRM from your legally purchased EPUB files and read them on any device, including Kindle.

---

## ⚠️ Legal Notice

> **This tool is for personal and educational use only.**

### ✅ Permitted Uses
- Removing DRM from ebooks you have **legally purchased** for personal backup
- Converting your own library for device compatibility
- Educational study of digital rights management and cryptography

### ❌ Prohibited Uses
- Distributing, sharing, or selling DRM-free copies
- Removing DRM from content you do not legally own
- Any activity that violates copyright law in your jurisdiction

**You are solely responsible for ensuring your use complies with applicable laws.**

---

## 🔄 How It Works

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│  Purchase Book  │ ──▶ │  Download with  │ ──▶ │  Run Notebook   │
│  (.acsm file)   │     │  Adobe DE       │     │  (Remove DRM)   │
└─────────────────┘     └─────────────────┘     └────────┬────────┘
                                                         │
                                                         ▼
                        ┌─────────────────┐     ┌─────────────────┐
                        │  Read on Any    │ ◀── │  DRM-Free EPUB  │
                        │  Device         │     │                 │
                        └─────────────────┘     └─────────────────┘
```

### Prerequisites

1. **Adobe Digital Editions** - Install and sign in with your Adobe ID
2. **Python 3.8+** - With pip package manager
3. **Legally purchased ebooks** - Downloaded via Adobe Digital Editions

---

## 🚀 Quick Start

### 1. Setup Environment

```bash
# Create and activate virtual environment (recommended)
conda create -n acsm_kindle python=3.11
conda activate acsm_kindle

# Or use venv
python -m venv venv
source venv/bin/activate  # macOS/Linux
```

### 2. Download Your Books

1. Purchase an ebook (you'll get an `.acsm` file)
2. Open the `.acsm` file with Adobe Digital Editions
3. ADE downloads the DRM-protected `.epub` file
4. Copy the `.epub` from ADE's library to the `drm_epubs/` folder

**ADE Library Locations:**
- **macOS**: `~/Documents/Digital Editions/`
- **Windows**: `Documents\My Digital Editions\`

### 3. Run the Converter

1. Open `acsm_to_kindle_converter.ipynb` in VS Code or Jupyter
2. Run **Section 1** (Setup)
3. Run **Section 2** (Load Classes)
4. Run **Section 3** (Convert Books)

### 4. Send to Kindle

Your DRM-free EPUBs will be in `kindle_output/`. Upload them via [amazon.com/sendtokindle](https://www.amazon.com/sendtokindle)

> 💡 Modern Kindles (2022+) natively support EPUB!

---

## 📁 Project Structure

```
ACSM to Kindle/
├── acsm_to_kindle_converter.ipynb  # Main notebook
├── README.md                        # This file
├── drm_epubs/                       # INPUT: Place DRM-protected EPUBs here (from ADE)
├── kindle_output/                   # OUTPUT: DRM-free EPUBs ready for Kindle
└── device_keys/                     # ADE decryption keys (auto-extracted)
```

---

## 🔧 Troubleshooting

| Issue | Solution |
|-------|----------|
| **"No ADE keys found"** | Install Adobe Digital Editions, sign in, and download at least one book |
| **"Decryption failed"** | Ensure the EPUB was downloaded with the same Adobe ID as your ADE installation |
| **"No EPUB files found"** | Copy `.epub` files from ADE library to `drm_epubs/` folder |
| **Garbled text on Kindle** | DRM key mismatch - re-download the book with your authorized ADE |

---

## 🔐 Technical Details

### Adobe ADEPT DRM

Adobe's ADEPT (Adobe Digital Experience Protection Technology) uses:

- **RSA-1024**: Encrypts per-book AES content keys
- **AES-128-CBC**: Encrypts file contents
  - Zero IV for decryption
  - First 16 bytes after decrypt contain embedded IV (skipped)
- **PKCS7 padding**: Standard block cipher padding
- **zlib deflate**: Raw compression mode (wbits=-15)

### Key Storage

Your decryption key is stored in Adobe Digital Editions' `activation.dat` file:
- **macOS**: `~/Library/Application Support/Adobe/Digital Editions/activation.dat`
- **Windows**: `%APPDATA%\Adobe\Digital Editions\activation.dat`

The key is a base64-encoded PKCS#8 DER RSA private key.

---

## 📚 Dependencies

- `pycryptodome` - RSA and AES cryptography
- `ebooklib` - EPUB handling
- `beautifulsoup4` - HTML parsing
- `lxml` - XML parsing

Install via:
```bash
pip install pycryptodome ebooklib beautifulsoup4 lxml
```

---

## ⚖️ Legal Disclaimer

### Educational Purpose

This project is an educational demonstration of:
- Digital rights management (DRM) systems
- Cryptographic implementations (RSA, AES)
- EPUB file format structure
- Python programming techniques

### Personal Use Defense

In many jurisdictions, removing DRM for personal backup of legally purchased content is protected under:
- **US**: Fair use doctrine, DMCA Section 1201 exemptions
- **EU**: EUCD Article 6 with member state variations
- **General**: Format-shifting for personal use

### No Warranty

This software is provided "as is" without warranty of any kind. The authors:
- Make no guarantees about functionality or fitness for purpose
- Assume no liability for damages arising from use
- Do not endorse or encourage copyright infringement

### Your Responsibility

By using this software, you agree that:
1. You legally own or have authorized access to all ebooks processed
2. You will not distribute the resulting DRM-free files
3. You understand and accept all legal risks
4. You will comply with all applicable laws in your jurisdiction

---

## 🤝 Contributing

This is a personal educational project. Feel free to:
- Study the code to understand DRM and cryptography
- Adapt for your own personal use
- Report issues for educational discussion

**Do not** submit changes that facilitate piracy or copyright infringement.

---

## 📜 License

This project is provided for educational and personal use only. No formal license is granted for commercial use or redistribution.

---

## 🙏 Acknowledgments

- Adobe ADEPT protocol documentation from security research community
- DeDRM tools project for pioneering DRM research
- Python cryptography community

---

*Use responsibly. Respect creators and copyright.*
