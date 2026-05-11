Title: This is just an explaination of how i approached this data exfiltration Case . 
---

📝 Case Overview
A company suspects that an employee copied confidential files to a USB drive before leaving.  
This case documents the acquisition, preservation, analysis, and findings based on the provided evidence file:

`
suspect_file.zip
`

The goal was to simulate a real-world DFIR workflow while maintaining forensic integrity.

---

📁 Case Folder Structure
The following structure was created to organize evidence and maintain chain of custody:

`
CASE001/
│
├── EVIDENCE001/                 → Original suspect_file.zip
├── EVIDENCE001IMAGES/          → Forensic image (EVIDENCE001IMAGE.ad1)
├── EVIDENCE001_EXPORTEDFILES/   → Safely exported files from the image
├── CASE001_REPORTS/             → Notes, findings, documentation
└── CASE001_SCREENSHOTS/         → Screenshots taken during analysis
`

This structure ensures separation of original evidence, working copies, and analysis artifacts.

---

🔍 Tools Used
- FTK Imager – Evidence acquisition, imaging, hashing, and mounting  
- ExifTool – Metadata extraction  
- DB Browser for SQLite – Browser history analysis  
- Hexdump / strings / unzip – Deep file inspection  
- Mousepad / Notepad – Viewing text-based artifacts  

---

🧩 Evidence Identification
Three key evidence items identified inside the exported folder:

1. browser_history.sqlite  
   Relevance: Indicates online services accessed (e.g., cloud storage, file transfer sites).

2. CompanyFinancials2024.docx  
   Relevance: A confidential document allegedly copied to the USB.

3. usb_activity.log  
   Relevance: Provides a timestamped log of USB connection and file copy events.

Additional artifacts included:  
.recovered fragments, clientlist.xlsx, exitnotes.txt, filemetadata.json, screenshot1.png, holidayphotos.txt.

---

🖥️ Evidence Acquisition Process
1. Stored the original suspect_file.zip in EVIDENCE001/ without modification.  
2. Used FTK Imager to create a forensic image:  
   `
   EVIDENCE001_IMAGE.ad1
   `
3. FTK Imager automatically generated MD5 and SHA1 hashes to verify integrity.  
4. Mounted the .ad1 image read‑only to prevent alteration.  
5. Exported all files from the mounted image into EVIDENCE001_EXPORTEDFILES/.  
6. Transferred exported files to a forensic Kali machine for deeper analysis.

This workflow maintains forensic soundness and ensures the original evidence remains untouched.

---

🧪 Analysis Summary

1. Browser History (browser_history.sqlite)
Found two URLs:
- https://drive.google.com
- https://wetransfer.com

These are common data exfiltration platforms, supporting the suspicion of file transfer.

---

2. Exit Notes (exit_notes.txt)
Content found:

`
I have copied everything I need before leaving.
No one will notice since I used the USB late at night.
`

This is a direct admission of intent and strongly incriminating.

---

3. Metadata (file_metadata.json)
Shows creation details for two sensitive documents:

- CompanyFinancials2024.docx – Author: John Doe  
- client_list.xlsx – Author: Jane Smith  

Indicates these files originated from internal company systems.

---

4. Screenshot Metadata (screenshot1.png)
Key findings:
- File size only 25 bytes → corrupted or intentionally manipulated  
- Permissions: -rw-rw-rw- → insecure, suspicious  
- Warning: “PNG image did not start with IHDR” → malformed file  
- Timestamps align with other suspicious activity  

Possible explanations:
- Attempt to hide data  
- Fake screenshot  
- Corrupted evidence  

---

5. CompanyFinancials2024.docx
- File size: 174 bytes → far too small for a DOCX  
- Detected as text/plain, not DOCX  
- Likely a decoy or disguised file  
- Using strings, hexdump, and unzip, the real content was found:

`
CONFIDENTIAL Company Financial Summary 2024
Revenue: $4.5 Million
Projected Growth: 18%
New Client Acquisition Strategy: Internal Use Only
Prepared by: Finance Department
`

This confirms confidential data was present.

---

6. USB Activity Log (usb_activity.log)
Timeline extracted:

`
[2026-04-10 22:14:03] USB device connected
[2026-04-10 22:15:10] File copied: CompanyFinancials2024.docx
[2026-04-10 22:16:45] File copied: client_list.xlsx
[2026-04-10 22:20:01] USB device removed
`

This is direct evidence of data exfiltration.

---

7. Recovered Passwords (.recovered/passwords.txt)
Found credentials:

`
admin: admin123
finance: fin@2024
`

These may have been used to access restricted files.

---

🔐 Integrity Verification
Recorded hash values:

- MD5: de461f4711686163d49e6c91f264d0ac  
- SHA1: 1c75726934bbf476c8fdbab62805e3a0923becf4

Hashing ensures:
- Evidence was not altered  
- Acquisition process was forensically sound  
- Findings are admissible in court  

---

🚨 Suspicious Findings
- Evidence of file copying to USB at late hours  
- Access to cloud storage platforms  
- Confession note indicating malicious intent  
- Confidential financial data found inside disguised files  
- Manipulated or corrupted screenshot  
- Recovered passwords suggesting unauthorized access  

---

🧾 Conclusion
The forensic analysis strongly supports the suspicion that the employee copied confidential company files to a USB drive.  
Multiple artifacts — including logs, metadata, browser history, and the exit note — confirm intentional data exfiltration.

This case demonstrates:
- Proper evidence acquisition  
- Integrity preservation  
- Artifact analysis  
- Timeline reconstruction  
- Identification of malicious intent  

---

📚 Skills Practiced
- Evidence identification  
- Imaging & hashing  
- Metadata analysis  
- SQLite browser history analysis  
- File carving & deep inspection  
- Timeline reconstruction  
- Intent assessment  
- Documentation & reporting  

---
