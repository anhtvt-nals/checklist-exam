# 📘 Reservation Screen Specification

## 🎯 Purpose
Allow logged-in users to make an online reservation at a beauty clinic/store.

## 🖼️ Screen Summary
- Screen Name: Reservation from beauty store detail screen
- Access: Only logged-in users

## 📝 Fields

| Field Name               | Required | Input Type      | Format/Constraints                     |
|--------------------------|----------|------------------|-----------------------------------------|
| Beauty store name        | Yes      | Label            | Pre-filled                              |
| User name                | Yes      | Text             | 1–50 characters                         |
| User name (Kana)         | No       | Text             | Katakana only, 1–50 characters          |
| Gender                   | No       | Dropdown         | MALE, FEMALE, OTHER                     |
| Date of Birth            | No       | Date picker      | yyyy/mm/dd                              |
| Email                    | Yes      | Text             | Valid email, max 255 characters         |
| Phone number             | Yes      | Number input     | Digits only, 7–15 digits                |
| Start Date               | Yes      | Date picker      | yyyy/mm/dd                              |
| Start Time               | Yes      | Time picker      | hh:mm (24h format)                      |
| Estimated Time           | Yes      | Auto / Fixed     | Format: hh時間mm分 (e.g., 00時間30分)   |
| End Time                 | Auto     | Calculated       | Start Time + Estimated Time             |
| Note                     | No       | Textarea         | 15–1000 characters                      |

## 📅 Time Slot Rules

- Available: 7:00 – 20:00 in 30-minute blocks.
- Today and past dates: Disabled.
- Booked slots: Disabled.
- Offline working hours: Cannot select.
- Last available time: Working hours – estimated time.

## 🔐 Reservation Policy

- Only logged-in users can reserve.

---

# ✅ Self-Test Checklist

| ID  | Test Case Description | Input | Expected Output | Notes |
|-----|------------------------|-------|------------------|-------|
| HC01 | Fill all required fields correctly | Valid name, email, DoB, gender, phone, reservation date/time | Proceed to confirmation screen | Normal booking flow |
| HC02 | Optional field “User name Kana” is left empty | Empty | No validation error | Optional field |
| HC03 | Optional field “User gender” selected | MALE / FEMALE / OTHER | Saved successfully | Gender options available |
| HC04 | Optional field “User date of birth” filled in | yyyy/mm/dd | Saved successfully | Format validated |
| HC05 | Start date and time selected correctly (future date) | yyyy/mm/dd + hh:mm | End time auto-set correctly | End time = Start + estimated time |
| HC06 | Notes field filled with valid length (20 characters) | Valid note | Successfully saved | Within allowed range |
| HC07 | Calendar only allows future dates | Click on today/future | Past dates unselectable | Date restriction works |
| HC08 | Time slots auto disabled after selection | Select 10:00 slot | 10:00 becomes disabled for others | Time block enforced |
| HC09 | Displayed time blocks are in 30min increments | View blocks | Show 7:00 to 20:00 | Display format validated |
| HC10 | Press cancel button | Click "戻る" | Return to previous screen | Navigation correct |
| HC11 | Logged-in user can make reservation | Logged-in state | Reservation possible | Authentication passed |
| HC12 | Reservation duration is auto calculated correctly | Estimated time = 30 mins | End time = Start + 30 mins | Auto fill check |
| HC13 | Estimated time format validated | hh時間mm分 | Parsed and used correctly | Japanese format support |
| HC14 | Valid Kana input in Kana field | Katakana characters | Accepted | Full-width Katakana only |
| HC15 | Max valid phone number (15 digits) | 123456789012345 | Accepted | Format validated |
| HC16 | Min valid phone number (7 digits) | 1234567 | Accepted | Format validated |
| HC17 | Input all fields at max boundary | Max characters in all fields | Successfully submitted | Boundary test |

## ❌ Abnormal-Case Scenarios

| ID  | Test Case Description | Input | Expected Output | Notes |
|-----|------------------------|-------|------------------|-------|
| AC01 | Required fields left blank | Empty name/email | Validation error shown | Cannot submit |
| AC02 | Email exceeds 255 characters | Long string | Error message shown | Max length enforced |
| AC03 | Name field exceeds 50 characters | Long name | Error message shown | Limit enforced |
| AC04 | Note under 15 characters | "Short" | Validation error | Minimum length rule |
| AC05 | Phone < 7 digits | "123" | Validation error | Minimum digits rule |
| AC06 | Phone > 15 digits | Long string | Validation error | Maximum digits rule |
| AC07 | Invalid email format | "test@@mail" | Error message | Regex check |
| AC08 | Past date selected | 2022/01/01 | Not selectable | Disabled in calendar |
| AC09 | Today selected | Today's date | Not selectable | Blocked by restriction |
| AC10 | Invalid Kana characters used | "山田" | Validation error | Katakana only |
| AC11 | Malicious script in note | `<script>alert(1)</script>` | Rejected | XSS prevention |
| AC12 | Select reserved time slot | Already booked time | Disabled / error shown | Slot conflict check |
| AC13 | Select offline time slot | e.g. 06:30 | Not selectable | Rule enforcement |
| AC14 | Start time not set, try submitting | Missing time | Show error | Required field |
| AC15 | Invalid date format in manual input | 01/01/2022 | Validation error | Format = yyyy/mm/dd |
| AC16 | Invalid time format | 25:61 | Validation error | Format = hh:mm |
| AC17 | Special characters in name | "John@Doe" | Validation error | Alpha only expected |
| AC18 | Switch date without changing time | New date, old time | Time mismatch warning | Potential logic flaw |
| AC19 | Estimation time input with wrong format | "30min" | Parsing error | Require hh時間mm分 |
| AC20 | Duplicate booking in short interval | 10:00 and 10:10 | Block submission | Conflict detection |

## 📌 Additional Notes

- Time format: 24-hour clock (hh:mm)
- Date format: yyyy/mm/dd
- Kana input: Full-width Katakana only
- Phone number: Digits only, 7–15 length
- Email: Standard format, max 255 chars
- Note: 15–1000 characters
- Calendar restricts to future only
- Estimated time auto-fills end time
- Reservation only allowed if user is logged in
