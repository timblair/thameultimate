# UKU Membership Reconciliation Tool

A browser-based tool for UK Ultimate clubs to reconcile membership data between Spond Club and the UK Ultimate Association (UKU) membership system.

## Usage

1. Download `index.html`
2. Open it in any modern browser (Chrome, Firefox, Safari, Edge)
3. Upload your Spond member export (XLSX)
4. Upload your UKU/JustGo member export (CSV)
5. Select the appropriate columns for each field
6. Click "Compare Memberships" to see results
7. Export results to CSV if needed

No installation required - everything runs locally in your browser and no data is sent anywhere.

---

## Project Overview

This is a single-file HTML/JavaScript tool for reconciling membership data between two systems used by a UK Ultimate (frisbee) club:

1. **Spond Club** (https://www.spond.com/spond-club-overview/) - Used for managing player registration, session attendance, and club membership
2. **UK Ultimate Association (UKU) via JustGo** (https://ukultimate.justgo.com/) - The national governing body's membership system

The club is affiliated with UKU and receives public liability insurance through this affiliation. A requirement of affiliation is that all club members must have a paid annual UKU membership. The tool helps identify members who need to renew or obtain their UKU membership.

## Business Context

- The club has approximately 100 members
- The tool is used by the club administrator and club secretary
- It runs locally in a browser (no server required)
- Data exports are done manually every few weeks
- The UKU ID number is the primary key used to link records between systems

## Data Sources

### Spond Export
- **Format**: XLSX file
- **How to export**: `Members` → `Active Members` → select all → click `Export`
- **Key fields**:
  - First name and surname (separate columns)
  - UKU ID (collected during club registration)
  - Member email
  - Guardian 1 email (for under-18s)
  - Payment contact email
- **Note**: For junior members (under 18), the contact email may be a guardian's email rather than the member's own

### UKU/JustGo Export
- **Format**: CSV file
- **How to export**: `Club Reports` from main menu → `Members` category → `Club Members` report → `Export CSV`
- **Key fields**:
  - Member ID (UKU ID)
  - First name and surname (separate columns)
  - Email Address
  - Membership expiry date
- **Note**: The export includes ALL members ever associated with the club, including those with expired memberships

## Reconciliation Logic

The tool identifies five categories of issues:

1. **Matched** ✓ - Spond members with a UKU ID that matches an active (non-expired) UKU membership
2. **No Active UKU** - Spond members who have a UKU ID recorded, but that ID either doesn't exist in the UKU data or has an expired membership
3. **No UKU ID in Spond** - Spond members who haven't entered a UKU ID at all (may not have registered with UKU)
4. **UKU Not in Spond** - People in the UKU export (active OR expired) who don't appear in Spond (useful for cleaning up old UKU club affiliations)
5. **Data Mismatches** - Members who match on UKU ID but have different data (name, email) between the two systems

## Technical Details

### UKU ID Matching
- IDs are normalised before comparison: trimmed, lowercased, non-alphanumeric characters removed
- Leading zeroes are stripped (e.g., "00123" matches "123")
- This handles inconsistencies in how people enter their ID

### Date Handling
- Membership expiry dates determine whether a UKU membership is "active"
- Excel stores dates as serial numbers (days since 1900-01-01), which the tool handles
- Also supports DD/MM/YYYY (UK format) and YYYY-MM-DD formats
- A membership is considered expired if the expiry date is before today

### Email Fallback Logic
- For Spond members, the tool checks up to 3 email columns in priority order
- Uses the first non-empty email address found (must contain '@')
- Default priority: Member email → Guardian 1 email → Payment contact email

### Column Selection
- Users select which columns map to which fields via dropdowns
- The tool attempts to auto-detect columns based on common header names
- Preview functionality shows sample values to help verify correct column selection

## Output

### On-screen Results
- Summary statistics showing counts for each category
- Detailed tables for each issue category
- "UKU Not in Spond" table includes a "UKU Status" column (Active/Expired)

### CSV Export
- Single CSV file with all issues
- Columns: Category, Name, UKU ID, Email, Status, Details
- "Details" column used for data mismatch specifics

## Dependencies

- **SheetJS (xlsx.js)** - For reading Excel/CSV files, loaded from CDN: https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js

## Browser Compatibility

- Works in modern browsers (Chrome, Firefox, Safari, Edge)
- Runs entirely client-side; no data is sent to any server
- File downloads use Blob URLs (some browsers may block this on file:// protocol)

## Known Considerations

- The UKU export may include header rows that get counted; the tool handles this gracefully
- Date parsing preview shows dates in UK format (DD/MM/YYYY) via `toLocaleDateString('en-GB')`
- Empty expiry dates are treated as valid (no expiry)
