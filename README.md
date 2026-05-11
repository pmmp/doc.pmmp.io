PocketMine-MP Documentation
===========================

This repository contains the source files for https://doc.pmmp.io/.

The documentation is built and hosted by https://readthedocs.org/.

## Local Development

To build and preview the documentation locally, follow these steps:

### 1. Prerequisites
* **Python 3.12 or higher**
* **pip** (Python package installer)

### 2. Setup Environment (Recommended)
It is highly recommended to use a virtual environment to avoid conflicts:

#### Linux/macOS

```bash
python3 -m venv .venv
source .venv/bin/activate
```

#### Windows

For Command Prompt (cmd.exe):
```cmd
.venv\Scripts\activate.bat
```

For PowerShell:
```powershell
.\venv\Scripts\Activate.ps1
```

### 3. Install Dependencies
Install the required Sphinx extensions and themes:
```bash
pip install -r requirements.txt
```

> Note: Linux users may need to install `make` (e.g., `sudo apt install make`)

### 4. Build the Documentation

Once the setup is complete, run the build command:

#### Linux/macOS

```bash
make html
```

#### Windows

```bash
.\make.bat html
```

 The generated HTML files will be located in the `./build/html` directory. Open `./build/html/index.html` in your browser to view the site.


