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
| TC01 | Load screen with default settings        | N/A                              | Display latest campaigns sorted by date (default sort: newest) | Default initial state      |
| TC02 | Search by campaign name (kana)           | Search: "あい"                    | Display campaigns matching kana "あい" in title                 |                            |
| TC03 | Search by campaign name (romaji)         | Search: "tokyo"                  | Display campaigns containing "tokyo" in title                  |                            |
| TC04 | Filter by prefecture only                | Prefecture: Tokyo                | Show campaigns located in Tokyo                                |                            |
| TC05 | Filter by prefecture and city            | Prefecture: Tokyo, City: Shibuya | Show campaigns only from Shibuya, Tokyo                        | City depends on prefecture |
| TC06 | Filter by single category                | Category: Hair                   | Show only campaigns in Hair category                           |                            |
| TC07 | Filter by multiple categories            | Categories: Hair, Nail           | Show campaigns matching either Hair or Nail                    | OR logic                   |
| TC08 | Filter by prefecture, city, and category | Tokyo, Shibuya, Hair             | Show campaigns matching all criteria                           | AND logic                  |
| TC09 | Sort by newest                           | Sort: Newest                     | Campaigns sorted by created date descending                    | Default behavior           |
| TC10 | Sort by price ascending                  | Sort: Price Low to High          | Campaigns sorted by increasing price                           |                            |
| TC11 | Sort by price descending                 | Sort: Price High to Low          | Campaigns sorted by decreasing price                           |                            |
| TC12 | Pagination – next page                   | Click page 2                     | Load next 20 campaigns                                         |                            |
| TC13 | Pagination – go back                     | Click page 1                     | Load previous 20 campaigns                                     |                            |
| TC14 | Click campaign card                      | Click on any campaign            | Redirect to that campaign's detail page                        | Navigation test            |
| TC15 | Reset all filters                        | Apply filters → Click reset      | All filters cleared, list resets to newest campaigns           | Restore default            |
| TC16 | No filters selected                      | Leave all filters blank          | Show all campaigns                                             | Blank = no filtering       |                                                                                 | New campaigns from page 2 are shown                                            |

---

## 🟥 Abnormal / Edge Case Scenarios

| ID   | Test Case Description                      | Input                                          | Expected Output                                  | Notes                     |
| ---- | ------------------------------------------ | ---------------------------------------------- | ------------------------------------------------ | ------------------------- |
| TC17 | Search with no results                     | Search: "zzzz"                                 | Show “No campaigns found” message                | Valid input, no match     |
| TC18 | Search with special characters             | Search: "@#%"                                  | Show no results or safe default message          | Input should be sanitized |
| TC19 | Search with HTML/JS code                   | Search: `<script>`                             | Display sanitized input, no script executed      | XSS prevention            |
| TC20 | Filter with mismatched city and prefecture | Prefecture: Tokyo, City: Osaka                 | Show no results or auto-reset city               | Enforce dependency logic  |
| TC21 | Load screen with no internet               | Turn off network, load screen                  | Show error message or offline fallback           | Offline handling          |
| TC22 | Open page number with no results           | Page 100 when only 2 pages exist               | Show empty result or redirect to last valid page | Edge case                 |
| TC23 | No campaign image                          | Campaign with missing image                    | Show default/placeholder image                   | Graceful fallback         |
| TC24 | Campaign name too long                     | Name > 100 characters                          | Name truncated with ellipsis in UI               | UI constraint             |
| TC25 | All filters combined yield no result       | Prefecture: A, City: B, Category: C (no match) | Show “No campaigns found”                        | Logical combination error |

---

## 🔄 Notes
- Filters should persist across pagination.
- Search + filters should work in combination.
- All user inputs should be sanitized and escaped.
