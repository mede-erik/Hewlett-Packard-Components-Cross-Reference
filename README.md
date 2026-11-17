# Hewlett-Packard Components Cross-Reference

A comprehensive cross-reference database for Hewlett-Packard (HP) component part numbers, mapping HP part numbers to manufacturer part numbers (MPN) and alternative part numbers.

## Overview

This repository contains a curated cross-reference database for legacy HP/Agilent/Keysight electronic components, particularly semiconductor devices. The data is sourced from original HP documentation and compiled into a machine-readable CSV format for easy integration into BOM management systems, procurement workflows, and component substitution analysis.

## Data Source

### HP Semiconductor Components Reference (SEMIS)

**Document:** `docs/HP_SEMIS_4_1818_1826TYPES.pdf`

**Publisher:** Hewlett-Packard Company (HP)

**Publication Date:** December 10, 2003 (based on PDF metadata)

**Description:** This document is the "HP SEMIS 4 - 1818/1826 Types" semiconductor reference guide, covering HP part number series 1818-xxxx through 1826-xxxx. It was originally created using Acrobat 5.0 Scan Plug-in for Windows.

**Special Thanks:** We extend our gratitude to **Hewlett-Packard Company** (now split into HP Inc. and Hewlett Packard Enterprise, with the test & measurement division becoming Agilent Technologies and later Keysight Technologies) for publishing this comprehensive semiconductor cross-reference documentation. This historical document preserves critical component substitution data for legacy HP/Agilent/Keysight test equipment and instruments.

**Document Source:** The PDF file `HP_SEMIS_4_1818_1826TYPES.pdf` was generously provided by **Xdevs** (xdevs.com), a valuable resource for historical test and measurement equipment documentation. Thank you to Xdevs for preserving and sharing this critical HP semiconductor reference guide.

### HP Transistor-Diode Cross-Reference (QSL.net)

**Document:** `HP_Cross_Reference.txt` (from https://www.qsl.net/n9zia/hp/HP_Cross_Reference.txt)

**Publisher:** Hewlett-Packard Company (HP)

**Description:** Comprehensive transistor and diode cross-reference mapping HP part numbers to JEDEC numbers with manufacturer codes. This extensive database covers HP part series 1813-xxxx through 1966-xxxx, containing over 7,000 HP part numbers with manufacturer codes and JEDEC equivalents.

**Document Source:** The text file was generously provided by **N9ZIA (John Ackerman)** via his QSL.net amateur radio website (https://www.qsl.net/n9zia/hp/), which hosts a valuable collection of HP/Agilent test equipment documentation. Thank you to John Ackerman (N9ZIA) for preserving and sharing this critical HP transistor/diode cross-reference data.

### HP Part Number Cross-Reference (300 Series)

**Document:** `docs/300-hpxref.pdf`

**Publisher:** Hewlett-Packard Company (HP)

**Description:** HP 300-series part number cross-reference documentation covering HP part number mapping and substitution data.

**Document Source:** The PDF file `300-hpxref.pdf` was generously provided by **HP Archive** (https://hparchive.com/), an invaluable resource for preserving and sharing historical HP/Agilent/Keysight documentation. Thank you to HP Archive for making this critical cross-reference data available to the community.

## CSV Format

The cross-reference data is stored in `Cross_Reference.csv` with the following columns:

| Column | Description | Example |
|--------|-------------|---------|
| `HP PN` | Original Hewlett-Packard part number | `1820-0726` |
| `MPN` | Primary Manufacturer Part Number | `SN74199N` |
| `ALT MPN 1-6` | Alternative manufacturer part numbers (up to 6) | `74LS199`, `DM74LS199N` |
| `Description` | Component description | `Quad D-Type Flip-Flop` |
| `Package` | Package type | `DIP-16`, `SOIC-16` |
| `Manufacturer` | Original manufacturer | `Texas Instruments`, `National Semiconductor` |
| `Source Document` | Source PDF filename | `HP_SEMIS_4_1818_1826TYPES.pdf` |
| `Source Page` | Page number in source document | `5` |
| `Notes` | Additional notes or caveats | `Obsolete, use 74LS199` |

## Project Structure

```
Hewlett-Packard-Components-Cross-Reference/
├── Cross_Reference.csv          # Main cross-reference database
├── docs/
│   ├── HP_SEMIS_4_1818_1826TYPES.pdf  # Source document (scanned)
│   └── 300-hpxref.pdf                   # HP 300-series cross-reference
└── README.md                    # This file

**External Source:** QSL.net N9ZIA HP Cross-Reference (https://www.qsl.net/n9zia/hp/HP_Cross_Reference.txt)
```

## Usage

### Importing into Spreadsheet Applications

The CSV file can be opened directly in:
- Microsoft Excel
- Google Sheets
- LibreOffice Calc
- Any CSV-compatible tool

### Programmatic Access

```python
import csv

with open('Cross_Reference.csv', 'r') as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(f"HP PN: {row['HP PN']} -> MPN: {row['MPN']}")
```

### Database Import

For SQL databases:
```sql
CREATE TABLE hp_cross_reference (
    hp_pn VARCHAR(50) PRIMARY KEY,
    mpn VARCHAR(50),
    alt_mpn_1 VARCHAR(50),
    alt_mpn_2 VARCHAR(50),
    alt_mpn_3 VARCHAR(50),
    alt_mpn_4 VARCHAR(50),
    alt_mpn_5 VARCHAR(50),
    alt_mpn_6 VARCHAR(50),
    description TEXT,
    package VARCHAR(50),
    manufacturer VARCHAR(100),
    source_document VARCHAR(100),
    source_page INT,
    notes TEXT
);
```

## Contributing

### Adding New Cross-References

1. Ensure you have a verifiable source (HP/Agilent/Keysight documentation)
2. Add entries to `Cross_Reference.csv` following the established format
3. Include the source document and page number for traceability
4. Submit a pull request with your changes

### Processing Scanned Documents

The source PDF is a scanned document requiring OCR for text extraction. To extract data:

```bash
# Install OCR tools (example for Ubuntu/Debian)
sudo apt-get install tesseract-ocr python3-pip
pip install pytesseract pillow pymupdf

# Run OCR extraction script
python3 scripts/extract_ocr.py
```

## Data Integrity

- All entries should be verified against original HP documentation
- Part numbers follow HP's format: `XXXX-XXXX` (e.g., `1820-0726`)
- Manufacturer part numbers use standard industry formats
- Obsolete parts are marked in the Notes column

## License

This project compiles publicly available historical technical documentation. The original HP/Agilent/Keysight documents remain the intellectual property of their respective owners (HP Inc., Hewlett Packard Enterprise, Keysight Technologies). This cross-reference database is provided for educational and maintenance purposes only.

## Acknowledgments

| Document | Publisher | Date | Source | Notes |
|----------|-----------|------|--------|-------|
| HP SEMIS 4 - 1818/1826 Types | **Hewlett-Packard Company** | 2003-12-10 | **Xdevs (xdevs.com)** | Scanned via Acrobat 5.0 Scan Plug-in |
| HP 300-Series Cross-Reference | **Hewlett-Packard Company** | — | **HP Archive (hparchive.com)** | HP part number cross-reference |
| HP Transistor-Diode Cross-Reference | **Hewlett-Packard Company** | — | **N9ZIA QSL.net (qsl.net/n9zia/hp/)** | 7,000+ HP PNs to JEDEC |

**Special thanks to the engineers and technical writers at Hewlett-Packard, Agilent Technologies, and Keysight Technologies** who created and maintained these comprehensive component reference guides over decades. Their meticulous documentation enables the continued maintenance and repair of legacy test and measurement equipment worldwide.

**Additional thanks to Xdevs (xdevs.com)** for preserving and sharing this historical HP semiconductor documentation, making it available for the test equipment repair and maintenance community.

**Additional thanks to HP Archive (https://hparchive.com/)** for preserving and sharing the HP 300-series cross-reference documentation, providing a critical resource for HP part number mapping and substitution data.

**Additional thanks to John Ackerman (N9ZIA, https://www.qsl.net/n9zia/hp/)** for preserving and sharing the comprehensive HP transistor-diode cross-reference database, mapping over 7,000 HP part numbers to JEDEC equivalents with manufacturer codes.

---

*If you have additional HP/Agilent/Keysight component documentation to contribute, please open an issue or submit a pull request.*