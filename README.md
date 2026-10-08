# 📄 ATS Resume Checker

Upload your resume and get an **estimated ATS score**, a category breakdown, missing keywords,
prioritised fixes and example bullet rewrites. Built with **Streamlit** and **Google Gemini Flash**.

## Features
- Upload **PDF, DOCX or TXT** resumes
- Optional **job description** or **target role** for a more accurate keyword score
- Score breakdown: keyword match, content & impact, ATS-friendly formatting, section structure, readability
- Fast rule-based checklist (email, phone, links, sections, length, bullets, metrics)
- Prioritised improvements (High / Medium / Low) and before/after bullet rewrites
- Download the full report as Markdown

## How the score works
`Final score = 80% AI category score + 20% rule-based checklist score`

The AI score is a weighted average: keyword match 30%, content & impact 25%, formatting 20%,
structure 15%, readability 10%.

> ⚠️ **This is an estimate.** Real ATS tools (Workday, Greenhouse, Taleo, ...) do not publish a
> universal score. The AI also sees only the *extracted text*, not the visual layout.
> Use the score as guidance, not as a guarantee.

## Run locally
```bash
git clone https://github.com/<your-username>/ats-resume-checker.git
cd ats-resume-checker

python -m venv venv
# Windows: venv\Scripts\activate      Mac/Linux: source venv/bin/activate
pip install -r requirements.txt

streamlit run app.py
```

## Gemini API key
Get a free key at <https://aistudio.google.com/apikey>, then use **one** of these:

1. Paste it in the app sidebar (quickest), or
2. Create `.streamlit/secrets.toml` (never commit this file):
   ```toml
   GEMINI_API_KEY = "your-key-here"
   ```
3. Set an environment variable: `GEMINI_API_KEY=your-key-here`

The default model is `gemini-flash-latest`. If you see a "model not found" error, change the model
name in the sidebar (for example `gemini-2.5-flash`).

## Deploy on Streamlit Community Cloud
1. Push this repo to GitHub.
2. Go to <https://share.streamlit.io> and sign in with GitHub.
3. Click **Create app**, choose your repo, branch `main`, and main file `app.py`.
4. Open **Advanced settings → Secrets** and paste: `GEMINI_API_KEY = "your-key-here"`
5. Click **Deploy**.

## Troubleshooting
**`No module named 'pypdf'` (or `docx`, `google`)**
The package is not installed in the Python that runs Streamlit. The app now tries to install
missing packages automatically, but the reliable fix is to run these in your project folder:
```bash
python -m pip install -r requirements.txt
python -m streamlit run app.py
```
Using `python -m pip` and `python -m streamlit` makes sure both use the same Python.
If you use a virtual environment, activate it first.

- Install **`python-docx`**, not `docx`.
- **Streamlit Cloud:** `requirements.txt` must be in the repo root next to `app.py`. Then use
  **Manage app -> Reboot app**.
- **"Model not found":** change the model name in the sidebar (for example `gemini-2.5-flash`).
- **"API key rejected":** create a new key at <https://aistudio.google.com/apikey>.

## Privacy
Resume text is sent to Google's Gemini API for analysis. Nothing is stored by this app.
Don't upload documents you are not comfortable sharing.

## Limitations
- Scanned or image-only PDFs can't be read (an ATS couldn't read them either).
- Layout problems (columns, text boxes, icons) can only be inferred from the extracted text.
- AI output can occasionally be wrong. Only add keywords you can honestly back with real experience.

## Project structure
```
ats-resume-checker/
├── app.py
├── requirements.txt
└── README.md
```
