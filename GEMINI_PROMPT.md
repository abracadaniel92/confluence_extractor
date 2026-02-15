# Gemini Prompt for Formatting Release Notes

Use this prompt in Google Gemini to format the merged release notes into a structured format.

## Prompt

```
You are a technical writer tasked with formatting release notes from a merged text file. The file contains multiple release notes separated by clear markers.

Your task is to:
1. Parse the merged release notes file
2. Extract information for each release
3. Format it in a clean, structured markdown format

## Output Format

For each release, create a section with the following structure:

### Release [Version] - [Date]

**Release Information:**
- Version: [version number]
- Date: [release date]
- Description: [if available]

**New Features:**
- [Feature 1 description]
- [Feature 2 description]
- [Add more as needed]

**Improvements to existing features:**
- [Improvement 1]
- [Improvement 2]
- [Add more as needed]

**Bug Fixes:**
- [Bug fix 1 with issue key if available]
- [Bug fix 2 with issue key if available]
- [Add more as needed]

**Known Issues:**
- [Known issue 1 with workaround if available]
- [Known issue 2 with workaround if available]
- [Add more as needed]

---

## Instructions

1. Read through the entire merged release notes file
2. Identify each release by the "RELEASE X/Y:" markers
3. Extract the version number and date from the release title
4. Look for tables containing issue information (Issue, Summary, Issue Type, Description columns)
5. Categorize issues based on:
   - Issue Type (Story, Task, Bug, etc.)
   - Summary keywords (New, Added, Extended, Fixed, etc.)
   - Description content
6. Group similar issues together
7. Format issue keys (like SUP-123, AXM-456) as links or references
8. Extract any tables showing issues and include them in the appropriate sections
9. Look for sections already labeled as "New Features", "Improvements", "Bug Fixes", "Known Issues" and preserve that structure
10. If a release has a "Summary" section, use it to understand the overall theme
11. For known issues, include workarounds if mentioned
12. Maintain chronological order (oldest to newest or newest to oldest - your choice, but be consistent)

## Special Handling

- If an issue appears in multiple categories, place it in the most appropriate one
- Preserve issue keys (e.g., SUP-123, AXM-456) and make them searchable
- If descriptions are very long, summarize them while keeping key technical details
- For tables, convert them to bullet points or preserve as markdown tables
- Remove any "How to use this page" or instructional text that's not part of the actual release notes
- Remove duplicate information across releases

## Example Output Structure

```markdown
# Release Notes - [Product Name]

## Release 2.2.0 - February 11, 2026

**Release Information:**
- Version: 2.2.0
- Date: February 11, 2026

**New Features:**
- Added support for FORTLOX Key transponder
- Added support for FORTLOX cylinder
- Extended WaveNet functionality:
  - Test functionality now delivers battery state, signal quality and firmware
  - Search Router (Central Node) by Hostname
  - Replace Router (Central Node) by IP
  - Replace Router (Central Node) with the same IP

**Improvements to existing features:**
- [List improvements here]

**Bug Fixes:**
- Fixed slow programming & synchronization failures related to the embedded C++ library (AXM-11758)
- Fixed issue when TN5 FD knob can be incorrectly recognized (AXM-6524)
- Fixed AXM freeze when resetting a router node (AXM-11746)
- Fixed issues related to resetting SR30 in other projects (AXM-10936)
- Fixed wrong time being displayed in card personal audit trails (AXM-10520)
- Fixed empty Matrix issue when opening database from backup (AXM-11556)
- Fixed various data representation issues in Desktop UI
- Fixed programming issues with transponders showing battery warnings (AXM-9577)

**Known Issues:**
- "Emergency Open" functionality deactivated - potential issue with some AX/G2 hardware versions
- In rare cases, AX2Go cannot open the lock despite authorization (MS-878)
  - Error only occurred during initial installation so far
  - Workaround: Removing authorization and reassigning resolves the problem
- AX2Go invitation cannot be accepted in specific cases (AXM-11834)
  - Workaround: Uninstall AX2Go app and install it again
- NW88 router is not recommended
  - Version not optimized
  - Missing functions
- Changing IP of SmartRelay 3 Advanced via TCP not possible (AXM-11419)
- VN Host: No matrix update due to deactivated TID (AXM-11373)
- Issue updating from AXM Plus MC version (AA-328)
- Predefined card templates are not supported (AXM-11812)

---

[Continue with next release...]
```

## Notes

- Be consistent with formatting across all releases
- Use clear, concise language
- Preserve technical accuracy
- Group related items together
- Make issue keys easily searchable
- Include workarounds for known issues when available

Now, please format the provided release notes file according to these instructions.
```

## Usage

1. Open the merged release notes file (`ALL_RELEASES_MERGED_Deployment.txt`)
2. Copy its entire contents
3. Go to [Google Gemini](https://gemini.google.com/)
4. Copy the prompt above
5. Paste the prompt, then paste the release notes content
6. Ask Gemini to format it according to the instructions
7. Copy the formatted output and save it as a markdown file

## Tips

- You can ask Gemini to format in reverse chronological order (newest first) if preferred
- You can request specific formatting adjustments (e.g., more detailed descriptions, shorter summaries)
- If the output is too long, you can process releases in batches
- Save the formatted output as `FORMATTED_RELEASE_NOTES.md` for easy reference
