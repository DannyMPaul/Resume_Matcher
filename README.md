# 🎯 Smart Resume Keyword Matcher

This is a portfolio project that demonstrates a classical Natural Language Processing (NLP) pipeline to solve a real-world problem: automatically comparing a resume against a job description. It's built to run entirely offline, requires no API keys, and showcases a full-stack approach from data processing to a user-friendly web interface.

The core idea is to move beyond simple keyword counting. This tool uses semantic analysis to understand the context of a resume, providing a more intelligent match score.

## ✨ Key Features

- **📄 Smart PDF Parsing**: It reliably extracts text from various resume layouts, including multi-column formats, using `pdfplumber`. It's designed to handle modern resume templates gracefully.
- **🔍 Automatic Section Detection**: The tool heuristically identifies and separates the resume's content into **Skills**, **Experience**, and **Education** sections. This allows for a more granular analysis of where your qualifications align with the job.
- **🧠 Semantic Match Scoring**: Instead of just checking for keywords, it uses `TF-IDF` (Term Frequency-Inverse Document Frequency) and **Cosine Similarity**. This technique understands that words like "managing" and "managed" are related, leading to a more accurate score. It provides:
  - An overall match percentage.
  - A breakdown of match scores for each section.
- **📈 Gap Analysis**: It identifies the most important keywords from the job description that are missing from your resume. The keywords are ranked by their importance in the job description, so you can prioritize your resume updates effectively.
- **💾 Local History**: Every analysis is automatically saved to a local `history.json` file. This creates a persistent log of your comparisons, allowing you to track your application progress over time.
- **🖥️ Clean, Modern UI**: A two-tabbed web interface built with `Gradio` provides a smooth user experience for analyzing resumes and reviewing past results.

## ⚙️ How It Works

The project is organized into a four-phase pipeline, all orchestrated within the `Resume_Matcher.ipynb` notebook.

1.  **Phase 1: PDF Parsing & Sectioning**
    - The process starts by extracting raw text from the uploaded resume PDF. `pdfplumber` is used for its robustness with complex layouts.
    - The extracted text is then passed to a section detector, which uses a list of keywords (e.g., "Experience," "Skills," "Education") to split the text into standardized buckets.

2.  **Phase 2: NLP Scoring & Analysis**
    - The text from the resume and job description is preprocessed using `spaCy`. This involves lowercasing, removing common "stopwords" (like "the," "and"), and **lemmatization** (reducing words to their root form).
    - A `TfidfVectorizer` from `scikit-learn` converts the cleaned text into numerical vectors.
    - **Cosine Similarity** is then calculated between the resume and job description vectors to generate the match scores. This is done for the overall document and for each section individually.
    - Finally, it analyzes the TF-IDF scores of the job description's terms to find important keywords that are absent from the resume.

3.  **Phase 3: History & Persistence**
    - The results of each analysis (scores, filename, timestamp, missing keywords) are packaged into a dictionary.
    - This dictionary is appended to `history.json`, a simple and effective way to store data without needing a database. The application reads this file to populate the "History" tab.

4.  **Phase 4: Gradio User Interface**
    - The final phase is the UI. `Gradio` is used to create an interactive web application.
    - It features a main "Analysis" tab with inputs for the resume and job description, and outputs for the scores and missing keywords.
    - A second "History" tab displays the contents of `history.json` in a clean, sortable table.

## 🛠️ Tech Stack

- **Language**: Python 3.9+
- **Core NLP**: `spaCy` (for lemmatization) & `scikit-learn` (for TF-IDF and Cosine Similarity)
- **PDF Parsing**: `pdfplumber`
- **Web UI**: `Gradio`
- **Data Handling**: `pandas` & `json`

## 📦 Setup & Installation

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/your-username/Resume_Matcher.git
    cd Resume_Matcher
    ```

2.  **Install Python dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

3.  **Download the spaCy language model:**
    This model is required for the text preprocessing step.
    ```bash
    python -m spacy download en_core_web_sm
    ```

## 🏃 How to Run

1.  Open the `Resume_Matcher.ipynb` file in a Jupyter environment like Jupyter Lab or VS Code.
2.  Run the first code cell under **"Setup & Imports"**. It will verify that all dependencies are installed correctly.
3.  Proceed to the last cell in the notebook, which contains the `Gradio` UI code.
4.  Run that final cell to start the web server.
5.  Click the local URL provided in the output (usually `http://127.0.0.1:7860`) to open the application in your browser.

## 📁 Project Structure

```
Resume_Matcher/
├── sample_resumes/        # Folder with sample resumes for testing
├── Resume_Matcher.ipynb   # The main Jupyter Notebook containing all logic and the UI
├── requirements.txt       # A list of all the Python packages required
├── history.json           # A file that stores the history of all past results
├── README.md              # You are here!
└── LICENSE                # MIT License
```
