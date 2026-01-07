# Hubstaff API Docs Updater (Smart Version)

A browser-based tool that automatically compares the live Hubstaff API documentation against your Hubstaff API Assistant tool and generates step-by-step instructions to add any new endpoints.

## 🎯 What It Does

- **Reads the live Hubstaff API docs** - Parses the official OpenAPI/Swagger specification
- **Parses your actual tool** - Extracts endpoints directly from your `index.html` file
- **Finds the differences** - Identifies new endpoints and new categories
- **Generates copy-paste instructions** - Provides exact find-and-replace steps to update your tool

## ✨ Key Features

- **No manual syncing required** - Reads your actual file every time, so it's always accurate
- **Paste from GitHub** - No need to download files; just paste raw HTML directly
- **Copy buttons** - One-click copying for all code snippets
- **Visual diff** - Clear highlighting shows what to find and what to replace
- **Keyboard shortcuts** - Instructions include ⌘+F / Ctrl+F reminders

## 📋 Prerequisites

- Your Hubstaff API Assistant (`index.html`) stored somewhere accessible (local or GitHub)
- Terminal access to run a curl command
- A modern web browser

## 🚀 How to Use

### Step 1: Download Latest API Documentation

Open Terminal and run:

```bash
curl 'https://api.hubstaff.com/v2/docs' -o ~/Desktop/hubstaff-api-docs.json
```

This downloads the current API specification from Hubstaff.

### Step 2: Open the Updater Tool

Open `hubstaff-api-updater-smart.html` in your web browser.

### Step 3: Load Both Files

**For the API docs (left side):**
- Drag and drop `hubstaff-api-docs.json` onto the drop zone

**For your tool (right side), choose one option:**

**Option A - Drop File:**
- Drag and drop your `index.html` file

**Option B - Paste from GitHub:**
1. Go to your GitHub repository
2. Navigate to your `index.html` file
3. Click the **"Raw"** button
4. Select all (⌘+A / Ctrl+A) and copy (⌘+C / Ctrl+C)
5. Back in the updater, click **"📋 Or paste your index.html code directly"**
6. Paste into the text area
7. Click **"✨ Parse Pasted Code"**

### Step 4: Compare

Click the **"🔍 Compare & Find Changes"** button.

### Step 5: Follow the Instructions

For each new endpoint found, the tool provides:

1. **FIND this line** - Copy and use ⌘+F to locate in your file
2. **REPLACE with** - Copy the replacement code (includes the original line + new endpoint)

## 📊 Understanding the Results

| Stat | Meaning |
|------|---------|
| **Live API Endpoints** | Total endpoints in Hubstaff's current API |
| **In Your Tool** | Total endpoints in your API Assistant |
| **New Endpoints** | Endpoints that need to be added |
| **New Categories** | Entirely new API categories not in your tool |

## 🔄 When to Run This

- **Periodically** - Check monthly or quarterly for API updates
- **After Hubstaff announcements** - When they announce new API features
- **Before sharing your tool** - Ensure it's up-to-date

## 🛠️ How It Works (Technical)

1. **API Docs Parsing**: Reads the OpenAPI 3.0 spec from `hubstaff-api-docs.json`, extracting paths, methods, and descriptions

2. **Tool Parsing**: Uses regex to find the `apiKnowledge` object in your HTML and extracts all endpoint definitions

3. **Category Mapping**: Maps API tags (like `time_entries`) to your tool's category names (like `timeEntries`)

4. **Diff Generation**: Compares endpoint keys (`METHOD /path`) between both sources

5. **Instruction Generation**: For each missing endpoint, finds the last endpoint in that category and generates a find-replace instruction

## 📁 File Structure

```
hubstaff-api-updater-smart.html  # The updater tool (this file)
index.html                        # Your Hubstaff API Assistant
hubstaff-api-docs.json           # Downloaded API docs (temporary)
README.md                         # This documentation
```

## ⚠️ Troubleshooting

### "Could not parse the HTML"
- Make sure you're pasting the **complete** HTML file
- Check that your `index.html` contains `const apiKnowledge = {`
- Ensure there are no JavaScript syntax errors in your file

### "Could not find apiKnowledge object"
- The tool looks for `const apiKnowledge = {` in your HTML
- Make sure this object exists and is properly formatted

### Parse shows 0 endpoints
- Check that your endpoints follow the format:
  ```javascript
  { method: "GET", path: "/v2/...", desc: "..." }
  ```

### Copy button doesn't work
- Make sure you're using HTTPS or localhost (clipboard API requirement)
- Try a different browser if issues persist

## 🔮 Future Improvements

Potential enhancements:
- [ ] Fetch API docs directly (no curl needed)
- [ ] GitHub URL input (fetch raw content automatically)
- [ ] Export updated file directly
- [ ] Track update history

## 📝 License

Internal tool for Hubstaff support team use.

---

**Created with ❤️ to make API documentation maintenance easier**
