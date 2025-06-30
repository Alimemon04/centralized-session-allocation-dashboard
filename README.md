# Centralized Session Allocation Dashboard | BYJU’S Tuition Center

This project showcases an automated dashboard built in Google Sheets/Excel to match student extra-class requests with available recorded sessions based on partial keyword matching and metadata filtering (grade, board, language).

It replaced a manual, multi-sheet lookup process used by the BYJU’S Tuition Center operations team.

---

## 🧠 Problem Statement

Previously:

* Students submitted extra class requests via Google Forms.
* Operations team manually searched for topics across sheets based on grade, board, and language.
* Human errors (e.g., typos, inconsistent topic naming) and manual filtering created delays and inefficiencies.

---

## ✅ Solution Overview

A centralized dashboard with:

* **Search interface** to select Grade, enter a Topic Name, and choose a **minimum percentage match**
* **Automated filters** that pull and match topics based on keyword similarity
* **Dynamic matching threshold** (100% down to 15%) to allow flexibility

---

## 🔍 How It Works

### 🔸 Step 1: User Input (Search Topic Tab)

* `A3`: Grade Dropdown (e.g., 10th CBSE)
* `B3`: Topic to search (e.g., "Motion, Force and Work")
* `C3`: Match Threshold (e.g., 15%, 30%, ..., 100%)

### 🔸 Step 2: Keyword Match Logic

Each topic from the master list is evaluated using a partial keyword match formula:

```excel
=ARRAYFORMULA(SUM(IFERROR(MATCH("*"&split(TRIM('Search Topic'!$B$3)," ")&"*",D5,0),0)) / COUNTA(split(TRIM('Search Topic'!$B$3)," ")))
```

### 🔸 Step 3: Filtered Result (Cell A4 in 'Search Topic' Tab)

Based on Grade and Match %, the following nested IF logic filters the relevant results:

```excel
=IF(A3="10th CBSE", FILTER(CBSE1!AK2:AN1000, CBSE1!AO2:AO1000 > 0, CBSE1!AO2:AO1000 >= C3), ...)
```

This returns:

* Topic Name
* Raw Topic ID
* Video ID
* Match %

### 🔸 Step 4: Grade Dropdown Source (Cohort Tab)

The Grade dropdown in cell A3 on the Search Topic tab is dynamically populated using a helper table from the Cohort tab.

Logic:

* Grade and syllabus (e.g., Grade 7, CBSE) are concatenated to form options like Grade 7-CBSE.
* These values are then referenced in Data Validation for the grade selection.

Formula (used in column F of Cohort tab):

```excel
=CONCATENATE(E2,"-",A2)
```

This keeps the dropdown clean, standardized, and error-free for filtering purposes.

---

## 📂 Data Structure

* `CBSE` (Tab): Master database of all session topics and metadata
* `CBSE1` (Tab): Filtered list for each grade, enriched with % match
* `Search Topic` (Tab): UI for entering search criteria and viewing results
* `Cohort` (Tab): Maps grade and syllabus to dropdown-friendly format

---

## 📷 Screenshots

*(You can upload and embed screenshots here to show the UI in action)*

---

## 📄 Formula Logic & Breakdown

This project heavily uses Google Sheets formulas to calculate keyword match percentages, filter topics dynamically, and manage dropdowns.

You can explore the detailed logic in the [`formulas.md`](documentation/formulas.md) file.
---

📅 Project Timeline: Built in November 2022

---

🛠 Built & documented by Mohammad Ali Memon

For questions, suggestions or collaboration ideas — feel free to connect!
