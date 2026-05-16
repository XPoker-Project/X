# 🎯 X-Poker Daily Redeem Code - Customer Service Validation Guide

**Campaign Duration:** Ongoing Daily  
**Updated:** May 10, 2026  
**Code Source:** `redeem_codes.csv` (Dynamic, 700 codes total)

---

## 📋 **Code Format Overview**

### **Structure**
- **Format**: 3 uppercase letters + 4 numbers
- **Total Length**: 7 characters
- **Examples**: `MSK3421`, `DNQ9922`, `DAD3299`, `SML8757`

### **Security Features**
✅ **Random Generation**: Letters and numbers are randomly generated  
✅ **Day-Based Validation**: One digit in the 4-number section matches the day  
✅ **Position Randomization**: The day digit can appear at ANY position in the 4 numbers  
✅ **External Storage**: Codes stored in CSV file (not visible in HTML source)  
✅ **One-Time Use**: Each code can only be redeemed once  

---

## 🔐 **Quick Validation Guide**

### **Day Mapping**
| Day | Digit | Example Codes | Last 4 Digits |
|-----|-------|---------------|---------------|
| **Monday** | **1** | `MSK3421`, `LUK5791`, `TFX3081` | Contains `1` |
| **Tuesday** | **2** | `DNQ9922`, `FNS4802`, `LTE8210` | Contains `2` |
| **Wednesday** | **3** | `DAD3299`, `MZW9373`, `HWA9399` | Contains `3` |
| **Thursday** | **4** | `MTP4524`, `MQK0496`, `IZC0944` | Contains `4` |
| **Friday** | **5** | `FFJ8725`, `YTX5136`, `WTK4705` | Contains `5` |
| **Saturday** | **6** | `QJO6301`, `JNN7667`, `ZJB3566` | Contains `6` |
| **Sunday** | **7** | `SML8757`, `SRU6579`, `CWM5197` | Contains `7` |

### **Validation Logic**
- Extract the last 4 digits from the code
- Check if the day digit appears ANYWHERE in those 4 numbers
- The digit can be at position 1, 2, 3, or 4

**Examples:**
- `MSK3421` → Last 4: `3421` → Contains `1`? ✅ YES (position 4) → Monday code
- `DNQ9922` → Last 4: `9922` → Contains `2`? ✅ YES (positions 3 & 4) → Tuesday code
- `SML8757` → Last 4: `8757` → Contains `7`? ✅ YES (positions 3 & 4) → Sunday code

---

## ✅ **Step-by-Step Validation Process**

### **Step 1: Receive Code from User**
Customer submits code via chat/email (e.g., `MSK3421`)

---

### **Step 2: Validate Format**
**Check:**
- ✅ Total length = 7 characters
- ✅ First 3 characters = uppercase letters (A-Z)
- ✅ Last 4 characters = numbers (0-9)

**Examples:**
- `MSK3421` ✅ Valid format
- `msk3421` ❌ Invalid (lowercase letters)
- `MSK342` ❌ Invalid (only 6 characters)
- `M5K3421` ❌ Invalid (number in letter section)

---

### **Step 3: Check Day Digit**

**Process:**
1. Identify today's day of the week
2. Extract the last 4 digits from the code
3. Check if today's day digit appears in those 4 digits

**Example for Monday (digit = 1):**
```
Code: MSK3421
Last 4 digits: 3421
Day digit: 1
Position check: 3-4-2-1
                      ✅ Found at position 4!
Does it contain '1'? YES
Is today Monday? YES ✅ VALID
```

**Example for Tuesday (digit = 2):**
```
Code: DNQ9922
Last 4 digits: 9922
Day digit: 2
Position check: 9-9-2-2
                  ✅ ✅ Found at positions 3 & 4!
Does it contain '2'? YES
Is today Tuesday? YES ✅ VALID
```

---

### **Step 4: Verify Code in Database**

**Process:**
1. Open `redeem_codes.csv` file
2. Search for the exact code (e.g., `MSK3421`)
3. Check the `day` column

**CSV Structure:**
```
code,day,day_name
MSK3421,1,Monday
DNQ9922,2,Tuesday
DAD3299,3,Wednesday
```

**Validation:**
- ✅ Code found in CSV + `day` column matches today → VALID
- ❌ Code NOT found in CSV → FAKE/INVALID
- ❌ Code found but `day` column doesn't match today → WRONG DAY

---

### **Step 5: Check Redemption Status**

**Process:**
1. Open `redeem_codes_tracking.csv` (CS tracking file)
2. Search for the code
3. Check the `Redeemed` column

**Tracking File Structure:**
```
Code,Day,DayName,Redeemed,UserID,Timestamp,CSAgent,Notes
MSK3421,1,Monday,No,,,,,
DNQ9922,2,Tuesday,Yes,USER123,2026-05-09 14:32,Agent_Jane,First purchase
```

**Validation:**
- ✅ `Redeemed` = "No" → Code available, proceed
- ❌ `Redeemed` = "Yes" → Already used, reject

---

### **Step 6: Approve & Record**

**If ALL checks passed:**

1. **Update Tracking Spreadsheet:**
   - Change `Redeemed` from "No" to "Yes"
   - Fill in `UserID` (customer's ID/username)
   - Fill in `Timestamp` (current date/time)
   - Fill in `CSAgent` (your name/ID)
   - Add `Notes` (optional: "First deposit bonus", "Email redemption", etc.)

2. **Grant Reward:**
   - Process the redemption in the system
   - Credit user's account with the reward
   - Confirm with customer

3. **Response Template:**
   ```
   ✅ Code verified successfully!
   Code: MSK3421
   Reward: [REWARD DETAILS]
   Your account has been credited.
   Thank you for playing X-Poker!
   ```

---

## 🚨 **Common Rejection Reasons**

### **1. Wrong Format**
❌ **Issue:** Code doesn't match 3 letters + 4 numbers format  
**Examples:** `msk3421` (lowercase), `MSK342` (too short), `MSKR3421` (4 letters)  
**Response:** "Invalid code format. Please check and try again."

---

### **2. Wrong Day**
❌ **Issue:** Code's day digit doesn't match today  
**Example:** User submits `MSK3421` (Monday code with digit 1) on Tuesday  
**Response:** "This code is for Monday only. Today is Tuesday. Please check your code."

---

### **3. Code Not Found**
❌ **Issue:** Code doesn't exist in `redeem_codes.csv`  
**Response:** "This code is not valid. Please check for typos or contact support."

---

### **4. Already Redeemed**
❌ **Issue:** Code already used (Redeemed = "Yes" in tracking file)  
**Example:** 
```
Code: MSK3421
Redeemed: Yes
UserID: USER123
Timestamp: 2026-05-09 14:32
```
**Response:** "This code has already been redeemed on May 9, 2026. Each code can only be used once."

---

## 📊 **Daily Code Statistics**

**Total Codes:** 700  
**Codes per Day:** 100  

| Day | Codes Available | Day Digit |
|-----|-----------------|-----------|
| Monday | 100 | 1 |
| Tuesday | 100 | 2 |
| Wednesday | 100 | 3 |
| Thursday | 100 | 4 |
| Friday | 100 | 5 |
| Saturday | 100 | 6 |
| Sunday | 100 | 7 |

---

## 🎓 **Training Examples**

### **Example 1: Valid Monday Redemption**
```
Code: MSK3421
Format: MSK (letters) + 3421 (numbers) ✅
Last 4 digits: 3421
Contains '1'? YES (position 4) ✅
Today: Monday (day 1) ✅
In CSV: Yes, day=1 ✅
Redeemed: No ✅
RESULT: ✅ APPROVE
```

### **Example 2: Wrong Day**
```
Code: DNQ9922
Format: DNQ (letters) + 9922 (numbers) ✅
Last 4 digits: 9922
Contains '2'? YES ✅
Today: Friday (day 5) ❌
In CSV: Yes, day=2 (Tuesday) ❌
RESULT: ❌ REJECT - "This is a Tuesday code, today is Friday"
```

### **Example 3: Already Redeemed**
```
Code: DAD3299
Format: ✅
Day digit: 3 (Wednesday) ✅
Today: Wednesday ✅
In CSV: Yes ✅
Redeemed: YES (UserID: USER999, Date: 2026-05-08) ❌
RESULT: ❌ REJECT - "Code already used on May 8"
```

### **Example 4: Fake Code**
```
Code: ABC1234
Format: ABC (letters) + 1234 (numbers) ✅
Last 4 digits: 1234
Contains '1'? YES ✅
Today: Monday ✅
In CSV: NOT FOUND ❌
RESULT: ❌ REJECT - "Invalid code"
```

---

**Document Version:** 2.0  
**Last Updated:** May 10, 2026  
