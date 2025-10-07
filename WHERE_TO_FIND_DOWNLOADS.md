# Where to Find the Download Buttons

## Step-by-Step Guide

The download buttons appear at different levels depending on what you're viewing. Here's exactly where to find them:

---

### 🔵 Download Package Button (Blue Button)

This button downloads the **entire distribution package** (.whl, .tar.gz, etc.)

**Where to find it:**

1. Go to http://localhost:8000
2. Search for a package (e.g., type `requests` and press Enter)
3. You'll see a list of versions - click on **any version number** (e.g., `2.31.0`)
4. You'll see a list of distribution files like:
   - `requests-2.31.0-py3-none-any.whl`
   - `requests-2.31.0.tar.gz`
5. **Click on one of these distribution files** (click the link, not just the filename)
6. **NOW YOU SHOULD SEE:** A blue button at the top that says **"⬇️ Download Package"**

The URL will look like:
```
http://localhost:8000/project/requests/2.31.0/packages/d2/f4/.../requests-2.31.0-py3-none-any.whl/
```

---

### 🔗 Download File Link (Text Link)

This link downloads an **individual file** from within a package.

**Where to find it:**

1. Follow steps 1-5 above to get into a distribution package
2. You'll see a list of files inside the package, like:
   - `requests/__init__.py`
   - `requests/api.py`
   - `requests/sessions.py`
3. **Click on any of these files** to view its contents
4. **NOW YOU SHOULD SEE:** Next to "Report Malicious Package" there will be a link that says **"⬇️ Download File"**

The URL will look like:
```
http://localhost:8000/project/requests/2.31.0/packages/d2/f4/.../requests-2.31.0-py3-none-any.whl/requests/__init__.py
```

---

## Quick Test Path

Try this exact path to see the download button:

1. Go to: http://localhost:8000
2. Type: `flask`
3. Click on a version (e.g., `3.1.0`)
4. Click on: `Flask-3.1.0-py3-none-any.whl`
5. **You should see the blue "Download Package" button here!**
6. Then click on any file (e.g., `flask/__init__.py`)
7. **You should see the "Download File" link here!**

---

## Troubleshooting

### I don't see any button!

**Most common issue:** You're not going deep enough into the site.

- ❌ **NOT on the homepage** (http://localhost:8000)
- ❌ **NOT on the versions list** (http://localhost:8000/project/requests/)
- ❌ **NOT on the distributions list** (http://localhost:8000/project/requests/2.31.0/)
- ✅ **YES - Inside a distribution** (http://localhost:8000/project/requests/2.31.0/packages/.../filename.whl/)

### The button is there but doesn't work

- Try clearing your browser cache (Ctrl+F5)
- Make sure the server is running (you should see it in the terminal)
- Check the browser console for errors (F12)

### Still can't see it?

Make sure:
1. The Flask server is running (check the terminal - you should see "Running on...")
2. You've navigated to the correct level (inside a .whl or .tar.gz file)
3. Try a different browser to rule out caching issues

---

## Visual Flow

```
Homepage
  └─> Search for "requests"
       └─> Click version "2.31.0"
            └─> Click distribution "requests-2.31.0-py3-none-any.whl"
                 └─> 🔵 BLUE DOWNLOAD BUTTON APPEARS HERE! 🔵
                 └─> Click file "requests/__init__.py"
                      └─> 🔗 DOWNLOAD FILE LINK APPEARS HERE! 🔗
```

---

## Expected Appearance

### Package Download Button
Should look like:
```
[⬇️ Download Package]  ← Blue button with white text
```

### File Download Link
Should look like:
```
Report Malicious Package | ⬇️ Download File
```
