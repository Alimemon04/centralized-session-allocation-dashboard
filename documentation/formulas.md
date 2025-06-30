# Centralized Session Allocation Dashboard - Formula Reference

This `formulas.md` file documents all major formulas used in the **Centralized Session Allocation Dashboard** project. This helps developers, analysts, or operations team members understand and maintain the logic used in the Google Sheet.

---

## 🔹 1. Matching Logic (% Match Calculation)

**Used In:** `CBSE1` tab (columns like `% Match` for each grade)

### Formula:

```excel
=ARRAYFORMULA(SUM(IFERROR(MATCH("*"&SPLIT(TRIM('Search Topic'!$B$3)," ")&"*",D4,0),0))/COUNTA(SPLIT(TRIM('Search Topic'!$B$3)," ")))
```

Purpose:
* Compares each word in the search key (cell B3 of Search Topic) with the topic name.

* Calculates how many words from the query match.

* Divides it by the total number of words in the query to get a percentage.


## 🔹 2. Filtered Search Result
Used In: Search Topic tab, cell A4

### Formula:
```excel
=IF((A3="4th CBSE"),
  FILTER(CBSE1!A2:D1000,CBSE1!E2:E1000>0,CBSE1!E2:E1000>=C3),
IF(A3="5th CBSE",
  FILTER(CBSE1!G2:J1000,CBSE1!K2:K1000>0,CBSE1!K2:K1000>=C3),
IF(A3="6th CBSE",
  FILTER(CBSE1!M2:P1000,CBSE1!Q2:Q1000>0,CBSE1!Q2:Q1000>=C3),
IF(A3="7th CBSE",
  FILTER(CBSE1!S2:V1000,CBSE1!W2:W1000>0,CBSE1!W2:W1000>=C3),
IF(A3="8th CBSE",
  FILTER(CBSE1!Y2:AB1000,CBSE1!AC2:AC1000>0,CBSE1!AC2:AC1000>=C3),
IF(A3="9th CBSE",
  FILTER(CBSE1!AE2:AH1000,CBSE1!AI2:AI1000>0,CBSE1!AI2:AI1000>=C3),
IF(A3="10th CBSE",
  FILTER(CBSE1!AK2:AN1000,CBSE1!AO2:AO1000>0,CBSE1!AO2:AO1000>=C3),
  "false")))))))

```

Purpose:
* Based on selected grade (A3) and match threshold (C3), fetches relevant rows from the grade-specific range in CBSE1.


## 🔹 3. Import Data from Grade-Specific Sheets
Used In: CBSE tab (original consolidated data)

### Formula:
```excel
=IMPORTRANGE("sheet_url","Sheet1!A2:E")
```

Purpose:
* Pulls raw topic data from external grade-specific files into the main dashboard.

* Repeated for each grade.


## 🔹 4. Grade Dropdown Mapping
Used In: Cohort tab (Column F)

### Formula:
```excel
=E2 & "-" & A2
```
Purpose:
* Creates the dropdown list values (like Grade 10-CBSE) used in Search Topic tab.


## 🔹 5. CBSE1 Sheet (Constrained Summary Table)
Used In: CBSE1 tab

### Formula:
```excel
=ARRAY_CONSTRAIN(ARRAYFORMULA({CBSE!BP374:BQ735, CBSE!BZ374:CA735}), 362, 4)
```


Purpose:
* Combines filtered and calculated topic name + ID + match data from CBSE.

### Notes:
* Every tab and formula is interdependent and should not be broken while restructuring the sheet.

* Always validate sheet references (CBSE, CBSE1, Search Topic, etc.) before replicating.

