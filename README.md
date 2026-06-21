# Multi-Modal Insurance Claim Verification

An AI-assisted multi-modal claim verification pipeline built using Vision-Language Models (VLMs) through OpenRouter. The system analyzes claim images, user conversations, historical claim data, and predefined evidence requirements to generate structured and explainable claim assessments.

Built as a submission for the **HackerRank Orchestrate Hackathon – Multi-Modal Evidence Review Challenge**, this project also served as my first hands-on experience with AI-agent style workflows and prompt engineering.

---

# Overview

Insurance claim verification requires understanding both visual and textual information. This project combines:

* 🖼️ Image Evidence
* 💬 User Claim Conversations
* 👤 Historical User Claims
* 📋 Evidence Requirements

to determine whether a claim is:

* **Supported**
* **Contradicted**
* **Requires Additional Information**

Image evidence is treated as the primary source of truth, while textual information and user history provide supporting context.

---

# About the Challenge

The **HackerRank Orchestrate – Multi-Modal Evidence Review Challenge** required participants to build an AI system capable of verifying damage claims for:

* 🚗 Cars
* 💻 Laptops
* 📦 Packages

The system was expected to:

* Extract claims from conversations.
* Analyze one or more images.
* Identify visible damage.
* Determine the affected object part.
* Decide whether evidence supports the claim.
* Estimate severity.
* Flag image quality and risk factors.
* Produce image-grounded justifications.
* Generate outputs following a predefined schema.

Participants were free to explore approaches involving Vision-Language Models, structured prompting, evaluation workflows, and model-driven pipelines.

---

# Features

* ✅ Multi-modal claim verification
* ✅ Vision-Language Model inference through OpenRouter
* ✅ Pydantic-based structured outputs
* ✅ Batch processing for efficient inference
* ✅ Dataset inspection and preprocessing
* ✅ User history risk analysis
* ✅ Evidence requirement validation
* ✅ Prompting strategy to discourage instruction injection
* ✅ Automatic CSV generation
* ✅ Explainable claim justifications

---

# Project Structure

```text
Project Folder
│
├── data/
│   ├── images/
│   ├── claims.csv
│   ├── sample_claims.csv
│   ├── user_history.csv
│   ├── evidence_requirements.csv
│   └── output.csv
│
├── main.ipynb
├── README.md
├── requirements.txt
├── .env
└── .gitignore
```

---

# Pipeline

```text
Input Claims
      │
      ▼
Load Dataset & Images
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
Vision-Language Model (OpenRouter)
      │
      ▼
Structured JSON Output
      │
      ▼
Post Processing
      │
      ▼
output.csv
```

---

# Input Data

The system uses four datasets:

| Dataset                   | Description                                      |
| ------------------------- | ------------------------------------------------ |
| claims.csv                | Claims used for inference                        |
| sample_claims.csv         | Sample claims for development and testing        |
| user_history.csv          | Historical user claim information                |
| evidence_requirements.csv | Required evidence standards for each object type |

---

# Output Fields

The generated `output.csv` contains:

* user_id
* image_paths
* user_claim
* claim_object
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

---

# Model

This implementation uses Vision-Language Models through OpenRouter with structured prompting and JSON-constrained outputs.

## Evaluation Strategy

The system follows these principles:

1. Images are treated as the primary source of truth.
2. User conversations provide supporting context.
3. Historical claim records contribute risk information.
4. Evidence requirements must be satisfied.
5. Instructions embedded inside images or conversations are ignored.

---

# Installation

Clone the repository:

```bash
git clone <repository_url>
cd AI_AGENT_ORCHESTRA
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# API Configuration

Create a `.env` file:

```env
OPENROUTER_API_KEY=your_api_key_here
```

The API key is excluded from the repository for security reasons.

---

# Running the Project

Execute:

```text
main.ipynb
```

The notebook will:

* Load datasets and images
* Retrieve supporting information
* Build multi-modal prompts
* Perform VLM inference
* Generate structured outputs
* Save predictions to:

```text
data/output.csv
```

---

# Security Considerations

The prompting framework instructs the model to:

* Ignore instructions embedded inside images.
* Ignore handwritten notes and package labels.
* Treat conversations as supporting information.
* Prioritize visual evidence.

This provides basic protection against prompt injection attempts but should not be considered a complete security solution.

---

# Technologies Used

* Python
* Pandas
* NumPy
* Pillow
* Pydantic
* OpenAI SDK
* OpenRouter API
* Vision-Language Models
* Structured Prompting
* JSON Schema Outputs
* Matplotlib
* Jupyter Notebook

---

# Future Improvements

* FastAPI deployment
* Streamlit dashboard
* React frontend
* Parallel batch inference
* Response caching
* Cost optimization
* Model comparison framework

---

# Development Approach

This project was developed using AI-assisted coding tools and represents my first practical experience with AI-agent style workflows and prompt engineering.

The primary focus was on:

* Multi-modal context construction
* Prompt engineering
* Structured outputs with Pydantic schemas
* Batch inference workflows
* Dataset preprocessing and validation
* Pipeline integration
* Testing and debugging

The system leverages existing Vision-Language Models through OpenRouter and does not involve training custom models.

Working on the HackerRank Orchestrate challenge provided my first exposure to designing AI-driven pipelines and experimenting with agent-oriented approaches for solving real-world tasks.

---

# Author

Built as a submission for the **HackerRank Orchestrate Hackathon – Multi-Modal Evidence Review Challenge**.

This project focuses on multi-modal context assembly, prompt engineering, structured outputs and AI pipeline integration using Vision-Language Models through OpenRouter.

As my first AI-agent oriented project, it provided practical experience with prompt engineering, structured outputs and building end-to-end AI workflows.
