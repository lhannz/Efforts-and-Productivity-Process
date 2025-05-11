# CDR Consolidator

**Author:** Roland Panaligan  
**Date:** 2025-05-12

A simple, CLI-driven Python script to merge multiple Call Detail Record (CDR) text files into one tab-delimited output for easy ingestion into Power BI.

---

## 📋 Table of Contents

1. [Overview](#overview)  
2. [Features](#features)  
3. [Prerequisites](#prerequisites)  
4. [Installation](#installation)  
5. [Usage](#usage)  
6. [Script Breakdown](#script-breakdown)  
7. [License](#license)
8. [CDR Consolidator Python Code](#CDR-Consolidator-Python-Code)

---

## 🔍 Overview

This project automates the daily consolidation of CDR extracts by:

1. Prompting the user to select one or more `.txt` files via a GUI file picker.  
2. Reading all files as text to preserve data fidelity.  
3. Concatenating them into a single pandas DataFrame.  
4. Exporting the combined data as a tab-delimited `.txt` file for seamless Power BI loading.

---

## ✨ Features

- **Interactive File Selection** – Leverages Tkinter’s file dialog.  
- **Data Integrity** – Forces `dtype=str` to prevent type coercion.  
- **Performance** – Batch loads with `pd.concat()` for speed.  
- **BI-Friendly Output** – Exports with `\t` delimiter for native Power BI support.  
- **Console Logging** – Real-time progress and row counts.

---

## ⚙️ Prerequisites

- Python 3.8+  
- pandas  
- tkinter (usually included with standard Python)  

Install required packages via pip:

```bash
pip install pandas
```

## 💻 CDR Consolidator Python Code
```
#!/usr/bin/env python3
"""
Script: CDR Consolidator
Author: Roland Panaligan
Date: 2025-05-12

Purpose:
  1. Launch file picker for CDR .txt selection.
  2. Read files as text to preserve columns.
  3. Merge into one DataFrame.
  4. Export tab-delimited `.txt` for Power BI.
"""
import tkinter as tk
from tkinter import filedialog
import pandas as pd
from pathlib import Path

def main():
    # Initialize and hide main Tk window
    root = tk.Tk()
    root.withdraw()

    # Prompt file selection
    files = filedialog.askopenfilenames(
        title="Select CDR .txt files",
        filetypes=[("Text files", "*.txt"), ("All files", "*.*")]
    )
    if not files:
        print("⚠️ No files selected. Exiting.")
        return

    # Read each file as text
    dfs = [pd.read_csv(fp, sep=",", dtype=str) for fp in files]
    combined = pd.concat(dfs, ignore_index=True)

    # Export as tab-delimited
    out = Path(files[0]).parent / "lvcdrconsolidated.txt"
    combined.to_csv(out, sep="\t", index=False)
    print(f"✅ Saved: {out}")

if __name__ == "__main__":
    main()
