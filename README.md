# Two-Layer-QR-Manual-Attendance-System-(DEMO)


> **A Secure, Offline-First Academic Attendance Solution preventing Proxy Attendance without Biometrics.**

## 📋 Overview

This project is a functional prototype of the attendance system designed for **COLLEGES**. It demonstrates how to combine **Physical Gate Entry Logs** with **Classroom Manual Attendance** to create a tamper-proof attendance record.

This interactive demo simulates the entire ecosystem (Gate Scanner, Database, and Professor's App) within a single interface using **Gradio** and **Python**.

---

## 🛡️ The Core Logic (Anti-Proxy Architecture)

The system relies on a **Two-Factor Verification** method to validate presence:

| Scenario | Gate Scan (Level 1) | Professor Mark (Level 2) | Final Status | System Action |
| --- | --- | --- | --- | --- |
| **Ideal Student** | ✅ Scanned | ✅ Marked Present | **✅ PRESENT** | Attendance Logged. |
| **Proxy Attempt** | ❌ No Scan | ✅ Marked Present | **❌ ABSENT** | **Flagged:** "Proxy Blocked". |
| **Bunking** | ✅ Scanned | ❌ Not Marked | **❌ ABSENT** | **Flagged:** "Bunking". SMS Triggered. |
| **Absent** | ❌ No Scan | ❌ Not Marked | **❌ ABSENT** | Standard Absence. |

---

## 🚀 How to Run this Demo

1. **Open in Google Colab:** [Link to your Notebook]
2. **Run the Code Cell:** Click the **Play (▶️)** button on the main code block.
3. **Wait for Installation:** The system will install `fastapi`, `uvicorn`, and `gradio`.
4. **Launch UI:** Scroll down to the bottom of the output area to see the interactive dashboard.

---

## 🧪 Testing Scenarios

Follow these steps to test the logic constraints:

### Scenario A: The Valid Student

1. Go to the **👮 Gate Security** tab.
2. Select Student **`22XU1A0501`** and click **"模拟 SCAN QR"**.
3. Go to the **👨‍🏫 Professor App** tab.
4. Check the box for **`22XU1A0501`**.
5. Click **Submit Attendance**.
6. *Result:* Status is **PRESENT**.

### Scenario B: The Proxy Attempt (The "Friend" mark)

1. **Do NOT** scan Student **`22XU1A0502`** at the Gate.
2. Go to the **👨‍🏫 Professor App** tab.
3. Check the box for **`22XU1A0502`** (pretending their friend is marking them).
4. Click **Submit Attendance**.
5. *Result:* Status is **ABSENT** with note **"PROXY BLOCKED"**.

### Scenario C: The Bunking Student

1. Go to the **👮 Gate Security** tab.
2. Scan Student **`22XU1A0503`**.
3. Go to the **👨‍🏫 Professor App** tab.
4. **Uncheck** (or do not select) **`22XU1A0503`** (they are not in class).
5. Click **Submit Attendance**.
6. *Result:* SMS Log will show an alert: *"SMS to Guardian: Your ward is absent."*

---

## 🛠️ Technology Stack (Demo Version)

* **Language:** Python 3.10+
* **Interface:** Gradio (Simulating Mobile App & Gate Device)
* **Database:** SQLite (In-memory/Local file `csi_wits_demo.db`)
* **Data Processing:** Pandas (For Ledger visualisation)

## 📱 Production Architecture (Full Scale)

*Note: This demo simulates the logic. The actual production deployment involves:*

* **Backend:** FastAPI (REST API)
* **Mobile App:** Python Kivy + Buildozer (Android APK)
* **Gate Hardware:** Raspberry Pi 4 + OpenCV
* **SMS:** Fast2SMS / Twilio API

---

