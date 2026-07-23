\# 🧪 SSCentral In-Game API — QA Audit \& Automation Suite



!\[Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge\&logo=postman\&logoColor=white)

!\[Newman](https://img.shields.io/badge/Newman-28A745?style=for-the-badge\&logo=node.js\&logoColor=white)

!\[JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge\&logo=javascript\&logoColor=black)

!\[GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-222222?style=for-the-badge\&logo=github\&logoColor=white)



This repository contains the complete automated test suite and QA audit documentation for the \*\*SSCentral In-Game API\*\* (v2). 



SSCentral is the backend platform supporting the mobile rhythm game \*\*\*FiveSteps: Rhythm Game\*\*\* (published on Google Play). This suite covers player authentication, song discovery, voting, hash verification, song downloads, and community pack browsing.



\---



\## 📊 Audit \& Regression Results Summary



The QA cycle consisted of an initial baseline audit followed by failure analysis, bug fixes, and a full regression test run.



| Test Metric | Initial Baseline Run | Final Regression Run |

| :--- | :---: | :---: |

| \*\*Total Requests\*\* | 69 | 69 |

| \*\*Total Assertions\*\* | 137 | 137 |

| \*\*Passed Assertions\*\* | 91 (66.4%) | \*\*137 (100%)\*\* |

| \*\*Failed Assertions\*\* | 46 (33.6%) | \*\*0 (0%)\*\* |

| \*\*Total Duration\*\* | 7.0s | 6.9s |

| \*\*Suite Outcome\*\* | ❌ Failed | ✅ Passed |



\---



\## 🖼️ Newman Execution Dashboards



\### Phase 1: Initial Baseline Audit (46 Failures Identified)

During the initial test execution, 46 assertions failed out of 137 due to backend defects and test assertion mismatches.



!\[Initial Audit Newman Summary](assets/initial-run-summary.png)



🔗 \*\*\[View Full Interactive Baseline Report (Live HTML)](https://YOUR\_GITHUB\_USERNAME.github.io/sscentral-api-qa-automation/reports/SSCentral-In-Game-API-Initial-Report.html)\*\*



\---



\### Phase 2: Final Regression Run (100% Pass Rate)

After fixing backend bugs and updating test script assertions, the full regression suite was executed, achieving a 100% pass rate.



!\[Regression Run Newman Summary](assets/regression-run-summary.png)



🔗 \*\*\[View Full Interactive Regression Report (Live HTML)](https://YOUR\_GITHUB\_USERNAME.github.io/sscentral-api-qa-automation/reports/SSCentral-In-Game-API-Regression-Report.html)\*\*



\---



\## 📂 QA Documentation



Detailed QA artifacts created during this testing project:



\* 📋 \*\*\[Test Plan (TEST\_PLAN.md)](docs/TEST\_PLAN.md)\*\* — Outlines test objectives, scope, environment setup, testing strategy, and exit criteria.

\* 🐛 \*\*\[Defect Report \& Failure Analysis (DEFECT\_REPORT.md)](docs/DEFECT\_REPORT.md)\*\* — Documents 5 representative issues (4 API defects + 1 test design mismatch) with root causes, fixes, and verification details.



\---



\## 🎯 Test Scope \& Coverage



The test suite contains \*\*69 requests\*\* organized into \*\*6 submodules\*\*:



| Folder / Module | Focus Area | Requests |

| :--- | :--- | :---: |

| \*\*00 - Player Authentication\*\* | Firebase Auth login \& JWT retrieval | 1 |

| \*\*01 - Song Discovery\*\* | Default feeds, search queries, pagination, and boundary parameters | 26 |

| \*\*02 - Voting\*\* | Song/pack voting, duplicate vote handling, unapproved song restrictions | 13 |

| \*\*03 - Hash Verification\*\* | SSC chart hash validation and route security checks | 15 |

| \*\*04 - Song Download\*\* | Downloading approved content and handling non-existent songs | 6 |

| \*\*05 - HUB \& Community Packs\*\* | Browsing featured and community-submitted song packs | 8 |



\---



\## 📁 Repository Structure



```text

sscentral-api-qa-automation/

├── assets/

│   ├── initial-run-summary.png       # Screenshot of baseline report dashboard

│   └── regression-run-summary.png    # Screenshot of regression report dashboard

├── docs/

│   ├── TEST\_PLAN.md                  # Comprehensive QA Test Plan

│   └── DEFECT\_REPORT.md              # Detailed Defect Log \& Failure Analysis

├── postman/

│   ├── SSCentral\_InGame\_API.postman\_collection.json  # Postman Collection

│   └── SSCENTRAL-LOCAL.postman\_environment.json      # Environment Variables (Sanitized)

├── reports/

│   ├── SSCentral-In-Game-API-Initial-Report.html     # Newman HTML extra report (Baseline)

│   └── SSCentral-In-Game-API-Regression-Report.html  # Newman HTML extra report (Regression)

└── README.md                         # Main repository overview

