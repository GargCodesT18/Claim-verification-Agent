# Evaluation Report

# Multi-Modal Insurance Claim Verification

## 1. Objective

The objective of this project is to automatically verify insurance damage claims using a combination of visual evidence, user claim descriptions, historical user information, and predefined evidence requirements.

The system produces structured outputs indicating whether a claim is supported, contradicted, or requires additional information while maintaining explainability and robustness against prompt injection attacks.

---

# 2. Model Configurations Evaluated

## Strategy 1 – Single Claim Inference

**Description**

* One claim processed per API request.
* Images and claim information evaluated independently.
* Simple implementation with minimal preprocessing.

### Advantages

* Easy debugging
* Clear response mapping
* Simple prompt structure

### Limitations

* Higher API overhead
* Increased runtime
* Lower throughput

---

## Strategy 2 – Batch Inference (Final Strategy)

**Description**

* Multiple claims processed in a single request.
* User history, evidence requirements, and images grouped together.
* Structured prompt designed to return JSON for every claim.

### Advantages

* Reduced API calls
* Better TPM utilization
* Lower latency
* Lower operational cost
* Higher processing efficiency

This strategy was selected for the final implementation.

---

# 3. Prompt Design

The prompt follows several strict evaluation rules:

* Images are treated as the primary source of truth.
* User conversations provide supporting context only.
* User history contributes risk information.
* Evidence requirements must be satisfied before approving a claim.
* Instructions embedded inside images, handwritten notes, or package labels are ignored to prevent prompt injection.

The model is instructed to return only structured JSON using predefined values.

---

# 4. Processing Pipeline

```
Claims CSV
      │
      ▼
Load Images
      │
      ▼
Retrieve User History
      │
      ▼
Retrieve Evidence Requirements
      │
      ▼
Build Multi-Modal Prompt
      │
      ▼
Vision Language Model
      │
      ▼
JSON Parsing
      │
      ▼
Output DataFrame
      │
      ▼
output.csv
```

---

# 5. Output Validation

The generated output is validated against the required schema.

Each prediction contains:

* evidence_standard_met
* evidence_standard_met_reason
* risk_flags
* issue_type
* object_part
* claim_status
* claim_status_justification
* supporting_image_ids
* valid_image
* severity

Only predefined values are accepted for categorical fields.

---

# 6. Operational Analysis

| Metric             | Value                |
| ------------------ | -------------------- |
| Model              | Gemma 3 27B (Vision) |
| Inference Strategy | Batch Processing     |
| Batch Size         | 4 Claims             |
| Temperature        | 0                    |
| Max Tokens         | 2500                 |
| Top P              | 0.9                  |

---

# 7. Runtime Analysis

The implementation uses batched inference to reduce repeated API calls and improve throughput.

Advantages include:

* Reduced request overhead
* Better token utilization
* Faster execution compared to single claim processing
* Lower overall inference cost

---

# 8. Image Usage

Each claim may contain one or more images.

Images are:

* Loaded locally
* Converted to RGB format if required
* Compressed as JPEG
* Base64 encoded
* Passed to the Vision-Language Model

This preprocessing ensures compatibility across multiple image formats.

---

# 9. Error Handling

The system includes fallback mechanisms for API failures.

If inference fails:

* Manual review is requested
* Claim status is set to `not_enough_information`
* Severity is marked as `unknown`
* Risk flag is set to `manual_review_required`

This guarantees that every input claim produces a valid output row.

---

# 10. Security Considerations

The implementation incorporates prompt injection protection.

Ignored instruction sources include:

* User conversations
* Handwritten notes
* Package labels
* Image text instructions

Only visible damage evidence is used for claim verification.

---

# 11. Final Strategy

The final solution uses:

* Multi-modal Vision-Language reasoning
* Structured prompting
* Batch inference
* User history integration
* Evidence requirement validation
* JSON-constrained outputs
* Robust fallback handling

This approach provides an efficient, explainable and scalable solution for automated insurance claim verification.
