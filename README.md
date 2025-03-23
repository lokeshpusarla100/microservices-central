

# 📄 **Project Plan & Feature Document**  
## ✅ **Feature: Purchase Bill / Invoice Data Extraction and Stock Update System**

---

## **1. Project Summary**  
This system helps businesses automatically extract product and purchase details from printed bills/invoices and directly update stock in their inventory database. This reduces manual entry, saves time, and improves accuracy.

---

## **2. MVP Features – Detailed Explanation (Top 5 Features)**  

### **1️⃣ Invoice/Bill Upload (Multi-format)**
- Users upload their purchase invoices or bills (JPG, PNG, PDF).
- System accepts:
  - Single invoice or multiple invoices (batch processing).
- Uploaded files are stored in the cloud (AWS S3 / GCP Bucket).
- Ensures file validation (size limits, correct formats).

---

### **2️⃣ OCR-based Data Extraction**
- Extract product-related information using:
  - **Google Vision API / Tesseract OCR**
- Extraction targets:
  - **Product Name / Description**
  - **HSN/SAC code**
  - **Quantity (with unit detection like cases, pcs)**
  - **Rate per unit**
  - **Discount % if available**
  - **Total Amount**
  - **GST breakdown (CGST, SGST, IGST)**
- OCR pre-processing:
  - Denoising, Binarization, Skew correction for better accuracy.
- Output: Structured JSON ready for review.

---

### **3️⃣ Data Review, Editing, and Correction**
- Show extracted data in a clean, editable table/grid.
- Auto-highlight low-confidence fields for manual correction.
- Allow users to:
  - Edit product names, rates, and quantities
  - Map to their product SKUs (auto-suggestions from DB)
- Mandatory fields validation before submission.

---

### **4️⃣ Approval & Stock Update in Database**
- Once user approves:
  - System matches extracted products to **user’s inventory database**.
  - Updates:
    - **Stock Count** (Increment)
    - **Last Purchase Price**
    - **GST info**
- If a product is not found, the system can:
  - Prompt the user to create a new product entry
  - Or skip that product (based on user choice)
- Saves purchase data into **Purchase History Table**.

---

### **5️⃣ Activity Log & Summary Report**
- Logs every bill processed (invoice date, vendor, amount, etc.).
- Provides a downloadable report (PDF/Excel) of processed bills.
- Optional: Summary dashboard showing:
  - Total purchases today/this week/month
  - Top purchased products
  - Vendor-wise spending

---

## **3. Full Feature Set - Phase 2 (Scalable features for production)**

| No. | Feature | Detailed Description |
|----|---------|----------------------|
| ✅ 6 | **Batch Upload Support** | User uploads 10-50 bills at once; parallel OCR processing |
| ✅ 7 | **Template/Format Learning** | System remembers invoice layouts over time; improves accuracy |
| ✅ 8 | **Dynamic Field Detection** | Smart detection of columns even if order/wording changes |
| ✅ 9 | **Support 200+ Bill Formats** | Retail, wholesale, pharma, FMCG-specific formats |
| ✅ 10 | **Vendor Tracking** | Link each bill to a vendor; maintain vendor-wise purchase history |
| ✅ 11 | **Auto-Create Missing Products** | Optionally create new inventory products if not found |
| ✅ 12 | **Vendor Data Management** | Add/Edit vendor GSTIN, phone, address for record |
| ✅ 13 | **Product Matching with Confidence Score** | Suggest product mapping with confidence percentage |
| ✅ 14 | **Downloadable Reports** | Monthly, daily purchase reports downloadable anytime |
| ✅ 15 | **ERP / Accounting Software Integration** | API-ready architecture for Tally, Zoho, Marg in future |

---

## **4. Database Models Summary**
### **Product Table**
| Field          | Type        | Notes |
|----------------|------------|-------|
| Product ID     | String (PK) |      |
| Product Name   | String      |      |
| HSN/SAC Code   | String      |      |
| Current Stock  | Integer     | Auto-updated |
| Last Purchase Rate | Decimal |      |
| GST %          | Decimal     |      |

### **Vendor Table**
| Vendor ID | Vendor Name | GSTIN | Contact | Address |

### **Purchase History Table**
| Purchase ID | Vendor ID | Product ID | Date | Quantity | Rate | GST | Total |

---

## **5. Application Flow (Step by Step)**
1. **Login / Dashboard**
2. **Upload Bill/Invoice (single/multiple)**
3. **OCR runs - Data Extracted**
4. **Show Extracted Data for Review**
5. **User Edits, Corrects, and Approves**
6. **Stock Auto-Updated for Products**
7. **Purchase History Logged**
8. **Summary Report available**
9. **User can view vendor/product wise purchases**

---

## **6. Tech Stack**
| Layer        | Technology |
|-------------|-----------|
| **Frontend** | ReactJS / NextJS |
| **Backend** | NodeJS / Spring Boot |
| **OCR** | Google Vision / Tesseract |
| **Database** | PostgreSQL / MongoDB |
| **Storage** | AWS S3 / GCP Bucket |
| **Auth** | JWT / OAuth |
| **Deployment** | GCP / AWS |

---

## **7. Timeline & Milestones**
| Task                                | Duration |
|-------------------------------------|---------|
| OCR Integration                     | 1-2 Weeks |
| UI/UX for Upload & Review           | 1 Week |
| Database Design + Stock Update Logic| 1 Week |
| Testing / Iteration                 | 1 Week |
| Activity Log + Reports              | 3 Days |
| Phase-2 Features                    | 3 Weeks |

---

## ✅ **8. Final Output / Benefits**
✔️ **Zero manual entry** — Time saved  
✔️ **Accurate Stock Update** — Auto-updated inventory  
✔️ **Vendor & Purchase History Tracking**  
✔️ **Reports Ready** — For taxation, GST, and accounting  
✔️ **Expandable** — Future ERP integrations possible

---

## ✅ **9. Future Scope**
- Auto-GST return generation
- Mobile app version
- AI-driven reorder suggestions
- Vendor-wise credit management
- Cloud deployment with scaling

---

## ✅ **Deliverables**
- Working web app with stock update system
- Database schema
- API documentation
- Sample reports and activity logs

