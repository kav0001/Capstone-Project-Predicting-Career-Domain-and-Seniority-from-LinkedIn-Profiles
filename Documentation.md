# Capstone Project Roadmap & Checklist  
**Predicting Career Domain and Seniority from LinkedIn Profiles**

📅 **Project timeline:** Jan 12 – Jan 31  
🏁 **Final deadline:** January 31, 23:59  
---

## Project Status Overview (as of Jan 12)

- ✔️ Rule-based **Seniority** baseline implemented and validated (~93% accuracy)
- ✔️ Rule-based **Department** baseline implemented (~72% weighted accuracy)
- ⚠️ Key error patterns identified (Marketing ↔ Sales, BD ↔ Sales)
- ❌ End-to-end pipeline not yet implemented
- ❌ Second (ML-based) approach not yet implemented
- ❌ Final predictions, report, and presentation pending

---

## 1️⃣ End-to-End Pipeline (MANDATORY – Core Product)

> This is the **main deliverable** that turns models into a usable system.

### 1.1 Load & Parse LinkedIn CV JSON  
📅 **Deadline: Jan 14**

- [ ] Load CVs from JSON files  
- [ ] Extract all job positions per profile  
- [ ] Identify **current job**:
  - `status == "ACTIVE"`
- [ ] Resolve edge cases:
  - Multiple ACTIVE positions → select by most recent start date  
  - No ACTIVE position → fallback to:
    - latest end date  
    - or top / primary position if available
- [ ] Handle missing fields (title, dates, positions)

**Current status:** ❌ Not started

---

### 1.2 Unified Text Normalization  
📅 **Deadline: Jan 15**

- [ ] Implement **single shared preprocessing function**:
  - lowercasing  
  - diacritics removal  
  - punctuation → whitespace  
  - normalization of `& / | -`  
  - multilingual robustness (EN / DE / FR)
- [ ] Reuse this function for:
  - department prediction  
  - seniority prediction

**Current status:** ⚠️ Partially implemented (duplicated logic in notebooks)

---

### 1.3 Model Inference (Batch Prediction)  
📅 **Deadline: Jan 16**

- [ ] Integrate:
  - `predict_department()`  
  - `predict_seniority()`
- [ ] Batch inference over multiple CVs
- [ ] Allow switching between:
  - rule-based models  
  - ML-based models (later)

**Current status:** ❌ Not implemented as a unified pipeline

---

### 1.4 Output Format  
📅 **Deadline: Jan 16**

- [ ] Generate `predictions.csv` with columns:
  - `profile_id`
  - `job_title`
  - `predicted_department`
  - `predicted_seniority`
  - *(optional)* confidence / matched rules / explanation
- [ ] Validate format on unseen CVs

**Current status:** ❌ Not implemented

---

## 2️⃣ Second Modeling Approach (MANDATORY)

> Project requirement: **baseline + at least one additional approach**

### Option A (recommended): TF-IDF + Logistic Regression / Linear SVM

---

### 2.1 Supervised Model Training  
📅 **Deadline: Jan 19**

- [ ] Create fixed train/test split:
  - `random_state` fixed  
  - `stratify=y`
- [ ] TF-IDF feature extraction:
  - word n-grams (1–2)
  - `min_df` tuning
- [ ] Train **two separate models**:
  - department classification  
  - seniority classification
- [ ] Apply class weighting to handle imbalance

**Current status:** ❌ Not started

---

### 2.2 Model Interpretability  
📅 **Deadline: Jan 20**

- [ ] Extract top-weighted features per class
- [ ] Prepare examples for report:
  - “Top words driving Marketing / Sales / IT predictions”

**Current status:** ❌ Not started

---

## 3️⃣ Rule-Based Department Improvements (Quality Patch)

> Goal: fix **high-impact errors**, not perfect all edge cases.

---

### 3.1 Targeted Rule Refinements  
📅 **Deadline: Jan 18**

- [ ] Marketing ↔ Sales:
  - Handle `"Marketing & Sales"`, `"Sales and Marketing"`, `"Vertrieb und Marketing"`
  - Rule: if *marketing* appears → prioritize **Marketing**
- [ ] Business Development ↔ Sales:
  - partnerships / alliances / channels → **Business Development**
  - AE / SDR / quota / inside sales → **Sales**
- [ ] Project Management ↔ Marketing:
  - campaign / brand / comms → **Marketing**
  - scrum / pmo / delivery / jira → **Project Management**
- [ ] Add German / French synonyms for Sales, Marketing, BD

**Current status:** ⚠️ Error patterns identified, fixes not yet applied

---

### 3.2 Re-evaluation After Fixes  
📅 **Deadline: Jan 19**

- [ ] Updated classification report
- [ ] Confusion matrix
- [ ] Short error analysis (5–10 representative examples)

**Current status:** ⚠️ Baseline evaluated, not re-evaluated after fixes

---

## 4️⃣ Unified Evaluation & Model Comparison

---

### 4.1 Evaluation Protocol  
📅 **Deadline: Jan 21**

- [ ] Same data split for all models
- [ ] Metrics:
  - accuracy
  - macro F1
  - weighted F1
- [ ] Consistent reporting format

**Current status:** ⚠️ Implemented only for rule-based baselines

---

### 4.2 Model Comparison & Final Selection  
📅 **Deadline: Jan 22**

- [ ] Comparison table:
  - rule-based vs TF-IDF models
- [ ] Analysis:
  - where rules outperform ML
  - where ML outperforms rules
- [ ] Final decision:
  - single best model  
  - or hybrid (ML primary + rule-based fallback)

**Current status:** ❌ Not started

---

## 5️⃣ Predictions on Unseen CVs (MANDATORY)

---

### 5.1 Run on “More CVs to be predicted”  
📅 **Deadline: Jan 23**

- [ ] Execute final pipeline
- [ ] Save predictions CSV
- [ ] Verify schema and completeness

**Current status:** ❌ Not done

---

## 6️⃣ Final Documentation & Presentation

---

### 6.1 Final Report (PDF)  
📅 **Deadline: Jan 27**

**Required sections:**
- [ ] Problem definition & data
- [ ] Rule-based baselines
- [ ] Second modeling approach
- [ ] Model comparison
- [ ] Error analysis & limitations
- [ ] Role of GenAI (tools, prompts, usage)
- [ ] Contribution of each team member

**Current status:** ❌ Not started

---

### 6.2 Presentation (10 minutes)  
📅 **Deadline: Jan 29**

- [ ] 6–10 slides
- [ ] Clear storyline:
  - Problem → Baseline → Improvement → Results → Takeaways

**Current status:** ❌ Not started

---

## 7️⃣ Final Checks & Submission

📅 **Jan 30–31**

- [ ] Final pipeline run
- [ ] Reproducibility check
- [ ] Final PDF export
- [ ] Submission of all files

**Current status:** ❌ Pending

---

## Summary

- ✔️ Core rule-based logic implemented  
- ⚠️ Quality improvements partially done  
- ❌ Pipeline, ML approach, and packaging still ahead  
- 🔥 Highest risk items (time-critical):
  - End-to-end pipeline  
  - Final documentation

---

