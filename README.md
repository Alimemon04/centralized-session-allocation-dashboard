# Centralized Session Allocation Dashboard | BYJU’S Tuition Center

This project showcases an automated dashboard built in Google Sheets/Excel to match student extra-class requests with available recorded sessions based on partial keyword matching and metadata filtering (grade, board, language). 

It replaced a manual, multi-sheet lookup process used by the BYJU’S Tuition Center operations team.

---

## 🧠 Problem Statement

Previously:
- Students submitted extra class requests via Google Forms.
- Operations team manually searched for topics across sheets based on grade, board, and language.
- Human errors (e.g., typos, inconsistent topic naming) and manual filtering created delays and inefficiencies.

---

## ✅ Solution Overview

A centralized dashboard with:
- **Search interface** to select Grade, enter a Topic Name, and choose a **minimum percentage match**
- **Automated filters** that pull and match topics based on keyword similarity
- **Dynamic matching threshold** (100% down to 15%) to allow flexibility

---

## 🔍 How It Works

### 🔸 Step 1: User Input (Search Topic Tab)
- `A3`: Grade Dropdown (e.g., 10th CBSE)
- `B3`: Topic to search (e.g., "Motion, Force and Work")
- `C3`: Match Threshold (e.g., 15%, 30%, ..., 100%)

### 🔸 Step 2: Keyword Match Logic
Each topic from the master list is evaluated using a partial keyword match formula:

```excel
=ARRAYFORMULA(SUM(IFERROR(MATCH("*"&split(TRIM('Search Topic'!$B$3)," ")&"*",D5,0),0)) / COUNTA(split(TRIM('Search Topic'!$B$3)," ")))
