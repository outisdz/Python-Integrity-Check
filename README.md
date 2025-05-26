# Python Integrity Check

[![Python](https://img.shields.io/badge/Python-3.7%2B-blue.svg)](https://www.python.org/)
[![Rich Output](https://img.shields.io/badge/Output-Rich-6e4aff)](https://github.com/Textualize/rich)

## 🔍 Overview

**`integrity-check.py`** is a Python script for verifying file integrity.  
It generates a SHA-256 hash that includes both file contents and timestamp metadata, allowing you to detect tampering of both data and file attributes.  
You can create and check hash files, or verify against a provided hash digest, all from a simple command-line interface.

---

## ✨ Features

- **Hash Creation**: Generates a SHA-256 hash of a file, including:
  - File contents (read in chunks)
  - Creation time (`ctime`)
  - Last modification time (`mtime`)
  - Last access time (`atime`)
- **Integrity Verification**: 
  - Checks integrity using a stored hash file
  - Verifies directly against a provided SHA-256 digest (hex string)
- **Rich CLI Output**: Colored, user-friendly output using [Rich](https://github.com/Textualize/rich)
- **Interactive Prompts**: Prompts to overwrite files or specify names as needed

---

## 🛠️ Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/outisdz/Python-Integrity-Check.git
   cd Python-Integrity-Check
   ```

2. **Install dependencies:**
   ```bash
   pip install rich
   ```

---

## 🚀 Usage

Run the script directly with Python:

```bash
python integrity-check.py [OPTIONS]
```

### **Options & Arguments**

| Option / Argument         | Description                                                                |
|--------------------------|----------------------------------------------------------------------------|
| `-d`, `--destination`    | 📁 Where to store or read the hash file (default: current directory)        |
| `-s`, `--source`         | 📄 File to hash or check (required)                                        |
| `-c`, `--create`         | 🛠️  Create a hash file for the specified source file                       |
| `--check`                | 🔒 Check integrity of a file using its hash file                            |
| `--dhash`                | 🔑 Provide the hash (hex string) for direct checking                       |

> **Note:** Exactly **one** of `--create`, `--check`, or `--dhash` is required per run.

---

### **Examples**

#### 1. **Create a Hash File**
```bash
python integrity-check.py -s mydoc.pdf -c
```
This will create a hash file (`mydoc.pdf_hash256`) in the current directory.

#### 2. **Create a Hash File to a Custom Location**
```bash
python integrity-check.py -s myphoto.jpg -d ./hashes/ -c
```
If `./hashes/` is a directory, you will be prompted for a file name.

#### 3. **Check File Integrity Using a Hash File**
```bash
python integrity-check.py -s mydoc.pdf -d mydoc.pdf_hash256 --check
```

#### 4. **Check Integrity with a Provided Digest**
```bash
python integrity-check.py -s mydoc.pdf --dhash 3f4e2a...  # (Your hash here)
```

---

## 🧩 How Does It Work?

- Hashes file contents **and** its timestamp metadata (mtime, ctime, atime).
- Any change to file content or these timestamps will be detected.
- Uses [SHA-256](https://en.wikipedia.org/wiki/SHA-2) with [HMAC comparison](https://docs.python.org/3/library/hmac.html#hmac.compare_digest) for secure verification.
- All output is colorized and interactive via [Rich](https://github.com/Textualize/rich).

---

## ⚠️ Notes & Security

- **Hash files are binary**. Keep them safe and do not edit.
- Any change in file content **or** its metadata will result in a different hash.
- Do not rely solely on access/modification times for security — this is an integrity tool, not an anti-tamper solution.

---

## 📑 License

MIT License (see [LICENSE](LICENSE) if present).

---

## 🙏 Acknowledgments

- [Rich](https://github.com/Textualize/rich) for beautiful CLI output.
- Inspired by best practices in digital forensics.

---

## 💬 Feedback

Feel free to open [issues](https://github.com/outisdz/Python-Integrity-Check/issues) or pull requests!
