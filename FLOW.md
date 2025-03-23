
```mermaid
graph TD
    A[Start: User Login / Dashboard] --> B{Upload Bill or Invoice}
    B -- Single File --> C[Store File - AWS S3 or GCP]
    B -- Bulk Upload --> D[Batch Processing Queue]
    D --> C

    C --> E[OCR Processing using Tesseract or Google Vision]
    E --> F[Extract Text: Product, Quantity, Rate, GST]
    F --> G[Pre-process Data: Noise Removal, Skew Correction, Layout Detection]
    G --> H[Convert to Structured JSON]

    H --> I[Display Data in Editable Grid UI]
    I --> J{Highlight Low-Confidence or Missing Fields}
    J --> K[User Reviews and Edits Data]

    K --> L{Edit Product Details or Rates?}
    L -- Yes --> M[User Updates Fields]
    M --> N[Suggest Matching Product SKU from Database]
    N --> O{Is Product Found in Database?}
    L -- No --> O

    O -- Yes --> P[Auto Map Product Details]
    O -- No --> Q{Create New Product or Skip?}
    Q -- Create --> R[Prompt User to Add New Product]
    R --> S[Save New Product to Database]
    Q -- Skip --> P
    S --> P

    P --> T[Validate Mandatory Fields like Product and Rate]
    T --> U{Does User Approve Final Data?}
    U -- No --> K
    U -- Yes --> V[Update Database and Stock]

    V --> W[Increment Stock Count in Product Table]
    W --> X[Update Last Purchase Price]
    X --> Y[Update GST Details]
    Y --> Z[Insert Data into Purchase History]

    Z --> AA[Log Transaction Details like Vendor, Date, Amount]
    AA --> AB[Check Low Stock Alerts and Reorder Levels]
    AB --> AC[Generate Summary Reports or Export CSV]

    %% Phase 2 Features
    AC --> AD[Store User Corrections for AI Learning]
    AD --> AE[Improve Auto Suggestions for Next Upload]
    AE --> AF{ERP or Accounting Sync Required?}
    AF -- Yes --> AG[Sync with Tally, Zoho, or QuickBooks API]
    AF -- No --> AH[Skip Sync]

    AG --> AI[Store ERP Sync Logs]
    AH --> AI

    AI --> AJ[Notify User about Updates and Errors]
    AJ --> AK[Allow Vendor or Product-wise Purchase Analysis]

    AK --> AL{Are There More Bills to Process?}
    AL -- Yes --> B
    AL -- No --> AM[End Process: User Logout or Idle]

   style A fill:#000000,stroke:#fff,stroke-width:2px,color:#fff
    style AB fill:#000000,stroke:#fff,stroke-width:2px,color:#fff
    style B,J,L,O,Q,T fill:#ffffff,stroke:#000,stroke-width:1px, color:#000
    style C,D,E,F,G,H,I,K,M,N,R,S,P,U,V,W,X,Y,Z,AA fill:#ffffff,stroke:#000,stroke-width:1px, color:#000
