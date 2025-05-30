# 📘 US-CP01 Campaign List

## 🎯 Purpose
Allow users to browse, search, and filter beauty campaigns based on various conditions such as area, category, campaign type, and popularity.

## 🖼️ Screen Summary
- Screen Name: Campaign List Screen
- Access: Public

## 📝 Fields & UI Components

| Field Name               | Required | Input Type       | Format/Constraints                                |
|--------------------------|----------|------------------|----------------------------------------------------|
| Area filter              | No       | Dropdown         | Area list from DB                                  |
| Prefecture filter        | No       | Dropdown         | Filtered by area, dynamically loaded               |
| Category filter          | No       | Checkbox list    | Multiple selection                                 |
| Campaign Type filter     | No       | Checkbox list    | Multiple selection                                 |
| Sort By filter           | No       | Dropdown         | Options: 新着順 (Newest), 人気順 (Popular), etc.  |
| Keyword Search           | No       | Text input       | Supports Hiragana, Katakana, Kanji, alphanumerics |
| Campaign Cards           | -        | Visual List      | Displays image, title, price, store, location      |
| Pagination               | Auto     | Pagination nav   | Prev/Next with current page highlight              |
| Campaign Detail Button   | Yes      | Button/Link      | Navigates to campaign detail screen                |

---

# ✅ Self-Test Checklist

## 🟩 Happy Case Scenarios

| ID   | Test Case Description                    | Input                            | Expected Output                                                | Notes                      |
| ---- | ---------------------------------------- | -------------------------------- | -------------------------------------------------------------- | -------------------------- |
| HC01 | Load screen with default settings        | N/A                              | Display latest campaigns sorted by date (default sort: newest) | Default initial state      |
| HC02 | Search by campaign name (kana)           | Search: "あい"                    | Display campaigns matching kana "あい" in title                 |                            |
| HC03 | Search by campaign name (romaji)         | Search: "tokyo"                  | Display campaigns containing "tokyo" in title                  |                            |
| HC04 | Filter by prefecture only                | Prefecture: Tokyo                | Show campaigns located in Tokyo                                |                            |
| HC05 | Filter by prefecture and city            | Prefecture: Tokyo, City: Shibuya | Show campaigns only from Shibuya, Tokyo                        | City depends on prefecture |
| HC06 | Filter by single category                | Category: Hair                   | Show only campaigns in Hair category                           |                            |
| HC07 | Filter by multiple categories            | Categories: Hair, Nail           | Show campaigns matching either Hair or Nail                    | OR logic                   |
| HC08 | Filter by prefecture, city, and category | Tokyo, Shibuya, Hair             | Show campaigns matching all criteria                           | AND logic                  |
| HC09 | Sort by newest                           | Sort: Newest                     | Campaigns sorted by created date descending                    | Default behavior           |
| HC10 | Sort by price ascending                  | Sort: Price Low to High          | Campaigns sorted by increasing price                           |                            |
| HC11 | Sort by price descending                 | Sort: Price High to Low          | Campaigns sorted by decreasing price                           |                            |
| HC12 | Pagination – next page                   | Click page 2                     | Load next 20 campaigns                                         |                            |
| HC13 | Pagination – go back                     | Click page 1                     | Load previous 20 campaigns                                     |                            |
| HC14 | Click campaign card                      | Click on any campaign            | Redirect to that campaign's detail page                        | Navigation test            |
| HC15 | Reset all filters                        | Apply filters → Click reset      | All filters cleared, list resets to newest campaigns           | Restore default            |
| HC16 | No filters selected                      | Leave all filters blank          | Show all campaigns                                             | Blank = no filtering       |

---

## 🟥 Abnormal / Edge Case Scenarios

| ID   | Test Case Description                      | Input                                          | Expected Output                                  | Notes                     |
| ---- | ------------------------------------------ | ---------------------------------------------- | ------------------------------------------------ | ------------------------- |
| AC01 | Search with no results                     | Search: "zzzz"                                 | Show “No campaigns found” message                | Valid input, no match     |
| AC02 | Search with special characters             | Search: "@#%"                                  | Show no results or safe default message          | Input should be sanitized |
| AC03 | Search with HTML/JS code                   | Search: `<script>`                             | Display sanitized input, no script executed      | XSS prevention            |
| AC04 | Filter with mismatched city and prefecture | Prefecture: Tokyo, City: Osaka                 | Show no results or auto-reset city               | Enforce dependency logic  |
| AC05 | Load screen with no internet               | Turn off network, load screen                  | Show error message or offline fallback           | Offline handling          |
| AC06 | Open page number with no results           | Page 100 when only 2 pages exist               | Show empty result or redirect to last valid page | Edge case                 |
| AC07 | No campaign image                          | Campaign with missing image                    | Show default/placeholder image                   | Graceful fallback         |
| AC08 | Campaign name too long                     | Name > 100 characters                          | Name truncated with ellipsis in UI               | UI constraint             |
| AC09 | All filters combined yield no result       | Prefecture: A, City: B, Category: C (no match) | Show “No campaigns found”                        | Logical combination error |

---

## 🔄 Notes
- Filters should persist across pagination.
- Search + filters should work in combination.
- All user inputs should be sanitized and escaped.
