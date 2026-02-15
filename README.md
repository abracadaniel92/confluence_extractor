# Confluence Folder Extractor

A Python script to extract all pages from Confluence folders and export them to Word (.docx) and plain text (.txt) formats. Includes functionality to merge all exported files into a single combined document.

## Features

- ✅ Recursively extracts all pages from Confluence folders
- ✅ Exports each page to both Word (.docx) and plain text (.txt) formats
- ✅ Preserves original filenames from Confluence
- ✅ Extracts and formats tables (including issue tables)
- ✅ Handles expandable/collapsible sections
- ✅ Creates separate output directories for each folder
- ✅ Merge functionality to combine all releases into one file
- ✅ Supports multiple folder URLs in one run

## Prerequisites

### Required Python Packages

Install the required packages from the requirements file:

```bash
cd confluence_exports
pip install -r requirements.txt
```

This will install:
- `requests` - For Confluence API calls
- `beautifulsoup4` - For HTML parsing and table extraction
- `python-docx` - For Word document generation

### Required Files

1. **Tokens_txt.txt** - Must be in the same directory as the script or in the parent `Scripts/` directory
   - Contains Confluence API credentials
   - Format:
     ```
     CONFLUENCE_BASE_URL=https://your-instance.atlassian.net
     CONFLUENCE_API_EMAIL=your-email@example.com
     CONFLUENCE_API_TOKEN=your-api-token
     ```

### Getting Confluence API Token

1. Go to [Atlassian Account Settings](https://id.atlassian.com/manage-profile/security/api-tokens)
2. Click "Create API token"
3. Give it a label (e.g., "Confluence Extractor")
4. Copy the token
5. Add it to `Tokens_txt.txt`

## Installation

1. **Clone or download the script:**
   ```bash
   # Ensure confluence_folder_extractor.py is in your Scripts directory
   ```

2. **Set up credentials:**
   - Create or edit `Tokens_txt.txt` in the `Scripts/` directory
   - Add your Confluence credentials (see format above)

3. **Install dependencies:**
   ```bash
   cd confluence_exports
   pip install -r requirements.txt
   ```

## Usage

### Extract Pages from Confluence Folder

**Single folder:**
```bash
python confluence_folder_extractor.py "https://your-instance.atlassian.net/wiki/spaces/SPACEKEY/folder/FOLDERID"
```

**Multiple folders:**
```bash
python confluence_folder_extractor.py "url1" "url2" "url3"
```

**Example:**
```bash
python confluence_folder_extractor.py "https://simonsvoss.atlassian.net/wiki/spaces/SuperAdmin/folder/1898643458"
```

### Merge Exported Files

After extracting pages, merge them into a single file:

**Merge text files:**
```bash
python confluence_folder_extractor.py --merge "confluence_exports/Deployment" txt
```

**Merge Word documents:**
```bash
python confluence_folder_extractor.py --merge "confluence_exports/Deployment" word
```

## Output Structure

```
Scripts/
└── confluence_exports/
    └── [Folder Name]/
        ├── Release Notes - Version 1.0.0.docx
        ├── Release Notes - Version 1.0.0.txt
        ├── Release Notes - Version 2.0.0.docx
        ├── Release Notes - Version 2.0.0.txt
        ├── ...
        ├── ALL_RELEASES_MERGED_[Folder Name].txt    (after merge)
        └── ALL_RELEASES_MERGED_[Folder Name].docx   (after merge)
```

## How It Works

1. **Extraction:**
   - Parses the Confluence folder URL to extract folder ID
   - Uses Confluence REST API to fetch all pages in the folder
   - Recursively processes subfolders
   - Extracts content including tables and expandable sections
   - Exports each page to Word and text formats

2. **Table Extraction:**
   - Detects tables in both ADF (Atlassian Document Format) and HTML formats
   - Formats tables with proper column alignment
   - Preserves table structure in both output formats

3. **Merging:**
   - Combines all exported files from a folder
   - Adds clear separators between releases
   - Creates a single comprehensive document

## Configuration

### Credentials Location

The script looks for `Tokens_txt.txt` in:
1. Same directory as the script (`confluence_exports/`)
2. Parent directory (`Scripts/`)

### Output Directory

By default, files are exported to:
```
Scripts/confluence_exports/
```

This can be modified in the script by changing the `OUTPUT_BASE_DIR` variable.

## Troubleshooting

### Authentication Errors

**Error:** `Missing required credentials`

**Solution:**
- Check that `Tokens_txt.txt` exists and is in the correct location
- Verify the credentials are correctly formatted (no extra spaces, correct format)
- Ensure the API token is valid and not expired

### No Pages Found

**Error:** `No pages found in folder`

**Solution:**
- Verify the folder URL is correct
- Check that you have access to the Confluence space
- Ensure the folder ID in the URL is valid
- Try accessing the folder in your browser first

### Import Errors

**Error:** `ModuleNotFoundError: No module named 'requests'`

**Solution:**
```bash
cd confluence_exports
pip install -r requirements.txt
```

### Table Formatting Issues

If tables don't appear correctly:
- The script tries both ADF and HTML formats
- Some complex tables might not format perfectly
- Check the Word document version for better table rendering

### File Permission Errors

**Error:** `Permission denied` when writing files

**Solution:**
- Check that you have write permissions in the output directory
- Ensure the output directory exists or can be created
- On Windows, ensure files aren't open in another program

## Examples

### Extract Release Notes from Deployment Folder

```bash
cd Scripts/confluence_exports
python confluence_folder_extractor.py "https://simonsvoss.atlassian.net/wiki/spaces/SuperAdmin/folder/1898643458"
```

### Merge All Release Notes

```bash
cd Scripts/confluence_exports
python confluence_folder_extractor.py --merge "Deployment" txt
```

This creates `ALL_RELEASES_MERGED_Deployment.txt` with all releases combined.

## Next Steps

After merging the release notes:

1. **Format with Gemini:**
   - Use the `GEMINI_PROMPT.md` file as a guide
   - Upload the merged text file to Google Gemini
   - Get a formatted markdown output

2. **Review and Edit:**
   - Check the formatted output
   - Make any necessary adjustments
   - Save as a markdown file for documentation

## File Structure

```
confluence_exports/
├── confluence_folder_extractor.py    # Main script
├── requirements.txt                   # Python dependencies
├── README.md                         # This file
├── GEMINI_PROMPT.md                  # Prompt for formatting with Gemini
└── [Folder Name]/                    # Extracted folders
    ├── [Page 1].docx
    ├── [Page 1].txt
    ├── [Page 2].docx
    ├── [Page 2].txt
    └── ...
```

## Support

For issues or questions:
1. Check the troubleshooting section above
2. Verify your credentials and API token
3. Check Confluence API documentation: https://developer.atlassian.com/cloud/confluence/rest/

## License

ISC
