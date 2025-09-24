# Executable File Template

This is a template project for creating executable (.exe) files from Python applications. The user does not need to have Python set up or any project dependencies to run the executable.

## Project Structure

```
executable_file_template/
├── .gitignore                 # Git ignore rules (commented out as examples)
├── .streamlit/
│   └── config.toml           # Streamlit configuration
├── build/                    # Build artifacts (created during compilation)
├── data/
│   └── file.csv             # Sample data file
├── dist/                     # Distribution folder (final executable location)
├── hooks/
│   └── hook-streamlit.py    # PyInstaller hook for Streamlit
├── venv/                     # Virtual environment (for development)
├── main.py                   # Main application file
├── README.md                 # Project documentation
├── requirements.txt          # Python dependencies
├── run.py                    # Script to run the application
└── run.spec                  # PyInstaller specification file
```

## Important Note about .gitignore

**All entries in the `.gitignore` file are commented out intentionally.** These files and folders are kept in the remote repository as examples to demonstrate the necessary directory structure and file types required for creating executable files from Python projects.

In a real project, you should uncomment the relevant lines in `.gitignore` to properly ignore:
- Sensitive data files
- Virtual environment folders
- Build artifacts and executables
- Python cache files
- IDE configuration files
- OS-generated files

## Usage Instructions

### Step 1: Navigation and Environment Activation

```powershell
# 1.1 Navigate to the project
cd "C:\path\to\your\project"

# 1.2 Activate virtual environment
venv\Scripts\activate
```

### Step 2: Install/Update Dependencies

```powershell
# 2.1 Update pip
python.exe -m pip install --upgrade pip

# 2.2 Install PyInstaller specifically
pip install PyInstaller

# 2.3 Check PyInstaller version
pyinstaller --version

# 2.4 Install project dependencies
pip install -r requirements.txt

# 2.5 Install specific dependency (IF NEEDED)
pip install importlib-metadata
```

### Step 3: Create Necessary Folder Structure

```powershell
# 3.1 Create hooks folder (if it doesn't exist)
mkdir hooks

# 3.2 Create .streamlit folder (if it doesn't exist)
mkdir .streamlit

# 3.3 Verify structure
Get-ChildItem -Force
```

### Step 4: Create hook-streamlit.py File

### Step 5: Create config.toml File

### Step 6: Create run.py File (Launcher)

### Step 7: Create run.spec File 

### Step 8: Modify Your .main File (Add get_data_path function)

### Step 9: Check the Ports (8502) in use (VERY IMPORTANT!!!!)

```powershell
# 8.1 Check if port is in use
netstat -ano | findstr :8502

# 8.2 If there's a running process, terminate it
taskkill /F /IM run.exe

# 8.3 Verify again
netstat -ano | findstr :8502

# 8.4 Alternative cleanup using CMD on Windows
rmdir /s /q build dist 2>nul
```

### Step 10: Complete Cleaning (Historic Method)
```powershell
# 9.1 PowerShell specific cleaning
Remove-Item -Recurse -Force build, dist -ErrorAction SilentlyContinue

# 9.2 Verify cleaning
Get-ChildItem -Force

# 9.3 Alternative verification using CMD on Windows
dir /a
```

### Step 11: Build the Executable (With Detailed Log)
```powershell
# 10.1 Build with detailed information
pyinstaller run.spec --log-level INFO

# 10.2 Alternative CMD Windows (same command)
pyinstaller run.spec --log-level INFO

# 10.3 If error occurs, use debug mode
pyinstaller run.spec --log-level DEBUG

# 10.4 Verify if build was successful
Get-ChildItem dist
```

### Step 12: Test the Executable
```powershell
# 11.1 Navigate to dist folder
cd dist

# 11.2 List content
Get-ChildItem

# 11.3 Execute
.\run.exe

# 11.4 Alternative CMD Windows execution (example)
.\dist\run_immo_assist_app.exe

# 11.5 If need to terminate the process
taskkill /F /IM run.exe
```

### Step 13: Final Verification and Packaging
```powershell
# 12.1 Return to root
cd ..

# 12.2 Verify created file
Get-ChildItem *.zip

# 12.3 Alternative CMD Windows verification
dir /s *.zip
```

## 🔧 Troubleshooting Commands

### If Build Fails:
```powershell
# Check specific Streamlit dependencies
python -c "import streamlit; print(streamlit.__file__)"
python -c "import streamlit.web; import os; print(os.listdir(os.path.dirname(streamlit.web.__file__)))"

# Reinstall critical dependency
pip install importlib-metadata

# Build with detailed logs
pyinstaller run.spec --log-level DEBUG
```

### If Executable Won't Run:
```powershell
# Check running processes
netstat -ano | findstr :8502

# Terminate conflicting processes
taskkill /F /IM run.exe

# Try executing again
.\dist\run.exe
```

### Complete Cleanup (PowerShell):
```powershell
# Specific command from your history
Remove-Item -Recurse -Force build, dist -ErrorAction SilentlyContinue

# Verify cleanup
Get-ChildItem -Force
``` 

