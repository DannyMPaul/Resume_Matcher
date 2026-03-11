# 🎯 Smart Resume Keyword Matcher

A powerful, offline-first portfolio project that uses classical NLP to semantically compare Resume PDFs against Job Descriptions.

## 🚀 Concept
Most Applicant Tracking Systems (ATS) use simple keyword matching. This tool goes a step further by using **Word Lemmatization** and **TF-IDF Vectorization** to understand the content of your resume beyond exact word matches.

### Key Features
- **📄 Smart Parsing:** Extracts text from multi-column PDF layouts using `pdfplumber`.
- **🔍 Section Detection:** Automatically identifies Skills, Experience, and Education sections.
- **🧠 Semantic Scoring:** Uses TF-IDF and Cosine Similarity to provide an overall match score and a section-level breakdown.
- **📈 Gap Analysis:** Identifies the most important keywords from the Job Description that are missing from your resume.
- **💾 Local History:** Automatically saves every comparison to a local `history.json` for session-persistent tracking.
- **🖥️ Modern UI:** A clean, tabbed Gradio interface for easy interaction.

## 🛠️ Tech Stack
- **Language:** Python 3.9+
- **NLP:** `spaCy` (en_core_web_sm)
- **Scoring:** `scikit-learn` (TfidfVectorizer, cosine_similarity)
- **Parsing:** `pdfplumber`
- **UI:** `Gradio`
- **Data:** `pandas`, `json`

## 📦 Installation

1. **Clone the repository:**
   ```bash
   git clone <your-repo-link>
   cd Resume_Matcher
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Download spaCy model:**
   ```bash
   python -m spacy download en_core_web_sm
   ```

## 🏃 How to Run

1. Open `Resume_Matcher.ipynb` in Jupyter Notebook or VS Code.
2. Run the **Setup & Imports** cell to verify your environment.
3. Scroll to the bottom and run the **Gradio UI** cell.
4. Click the link (usually `http://127.0.0.1:7860`) to open the app in your browser.

## 📁 Project Structure
```text
Resume_Matcher/
├── Resume_Matcher.ipynb   # Main application (Logic + UI)
├── requirements.txt       # Python dependencies
├── history.json           # Local storage for past results
└── README.md              # Project documentation
```

---
*Created as a portfolio project to demonstrate NLP and full-stack Python development.*
