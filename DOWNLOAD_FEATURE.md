# Download Feature Implementation

## Overview
Added download functionality to Inspector to allow users to download packages and individual files directly from the web interface.

## What Was Added

### 1. Backend Routes (main.py)
Two new Flask routes were added:

#### `/project/<project_name>/<version>/packages/<first>/<second>/<rest>/<distname>/download`
- Downloads the entire distribution package (.whl, .tar.gz, .zip, .egg)
- Fetches the package from PyPI's file hosting
- Returns file with proper `Content-Disposition` header to trigger browser download

#### `/project/<project_name>/<version>/packages/<first>/<second>/<rest>/<distname>/<path:filepath>/download`
- Downloads individual files from within a package
- Extracts the file from the distribution archive
- Returns the file content with proper headers

### 2. Frontend Changes

#### Updated Templates:
1. **links.html** - Shows list of files in a package
   - Added "⬇️ Download Package" button at the top
   - Button downloads the entire distribution package

2. **code.html** - Shows individual file content
   - Added "⬇️ Download File" link next to "Report Malicious Package"
   - Downloads the currently viewed file

3. **disasm.html** - Shows decompiled Python bytecode
   - Added "⬇️ Download File" link
   - Downloads the original .pyc/.pyo file

#### Updated Styles (style.css):
- Added `.download-button` class - Blue button with hover effects for package downloads
- Added `.download-anchor` class - Styled link for file downloads

## How It Works

### Package Download Flow:
1. User browses to a distribution (e.g., requests-2.28.0-py3-none-any.whl)
2. Clicks "Download Package" button
3. Server fetches the package from `files.pythonhosted.org`
4. Browser downloads the complete package file

### File Download Flow:
1. User views a file within a package (e.g., `requests/__init__.py`)
2. Clicks "Download File" link
3. Server extracts the file from the cached distribution
4. Browser downloads just that file

## Benefits for Security Researchers

1. **Quick Access**: Download suspicious files for local analysis without manual PyPI navigation
2. **Offline Analysis**: Save packages/files for offline inspection with security tools
3. **Evidence Collection**: Easily archive malicious packages for reporting
4. **Workflow Integration**: Download files directly into analysis pipelines

## Testing

To test the feature:

1. Start the server:
   ```powershell
   .\.venv\Scripts\Activate.ps1
   $env:FLASK_APP = "inspector.main:app"
   flask run --host=0.0.0.0 --port=8000
   ```

2. Navigate to a package, e.g.:
   ```
   http://localhost:8000/project/requests/2.28.0/
   ```

3. Click on a distribution file (e.g., `.whl`)

4. You should see:
   - A blue "Download Package" button at the top
   - Click it to download the entire package

5. Click on any file within the package

6. You should see:
   - A "Download File" link next to "Report Malicious Package"
   - Click it to download just that file

## Technical Details

- Files are served with `Content-Type: application/octet-stream`
- Proper `Content-Disposition: attachment` headers trigger downloads
- Original filenames are preserved
- No additional dependencies required
- Works with all supported distribution formats (.whl, .tar.gz, .zip, .egg)
- Handles both text and binary files correctly

## Future Enhancements

Potential improvements:
1. Add download statistics/logging
2. Implement rate limiting for downloads
3. Add "Download All Files" option to download all files from a package as a ZIP
4. Add download size indication before downloading
5. Add keyboard shortcuts for quick downloads
