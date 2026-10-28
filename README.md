# Resume ATS Checker

A simple Streamlit application that accepts a resume and uses Google's Gemini Flash model to provide an **estimated ATS-readiness score**, strengths, prioritized improvements, job-description keyword matching, and example rewrites.

> **Important:** This is an educational estimate, not a score from an employer's actual Applicant Tracking System. Different employers and ATS products evaluate resumes differently. AI feedback may be imperfect; verify every suggestion and never add skills or experience you do not have.

## Features

- Upload a PDF, DOCX, or TXT resume (up to 5 MB).
- Optionally paste a job description for a more targeted review.
- Extracts text from supported documents.
- Shows basic text/section checks and word count.
- Uses Gemini Flash to generate an estimated score and actionable feedback.
- Download feedback as a Markdown file.
- API key is read from Streamlit Secrets or the `GEMINI_API_KEY` environment variable.

## 1. Get a Gemini API key

1. Open [Google AI Studio](https://aistudio.google.com/app/apikey).
2. Create an API key.
3. Keep the key private. Do not commit it to GitHub or put it directly in `app.py`.

## 2. Run locally

Use Python 3.10 or newer. In a terminal, from this folder:

```bash
python -m venv .venv
```

Activate the environment:

- Windows PowerShell: `.venv\\Scripts\\Activate.ps1`
- macOS/Linux: `source .venv/bin/activate`

Install packages:

```bash
python -m pip install -r requirements.txt
```

Set the API key for the current terminal session:

- Windows PowerShell: `$env:GEMINI_API_KEY="YOUR_API_KEY"`
- macOS/Linux: `export GEMINI_API_KEY="YOUR_API_KEY"`

Run the app:

```bash
streamlit run app.py
```

## 3. Push to GitHub using the website UI

1. Sign in at [GitHub](https://github.com/) and click **+** → **New repository**.
2. Give it a name such as `resume-ats-checker`. Choose Public or Private, then click **Create repository**.
3. In the new repository, choose **Add file** → **Create new file**.
4. Name the file `app.py`, paste the contents of your local `app.py`, and commit the file.
5. Repeat **Add file** → **Create new file** for `requirements.txt` and `README.md`; paste each file's contents and commit.
6. Check that all three files appear at the repository root. Never upload your API key, `.env` file, or real resumes.

You can also use **Add file** → **Upload files** to upload all three files from your computer in one commit.

## 4. Deploy on Streamlit Community Cloud

1. Push the three files to a GitHub repository.
2. Open [Streamlit Community Cloud](https://share.streamlit.io/) and sign in with GitHub.
3. Click **Create app** and select your repository, branch (usually `main`), and main file path `app.py`.
4. Open **Advanced settings** / **Secrets** before or during deployment and add:

```toml
GEMINI_API_KEY = "YOUR_REAL_API_KEY"
```

5. Save and click **Deploy**. Wait for installation and startup to finish.
6. Open the generated `*.streamlit.app` URL and test with a sample resume you have permission to use.

Keep the repository free of secrets. Streamlit's Secrets interface is the recommended place for the deployed API key. If you update the code and commit the changes to GitHub, Streamlit Community Cloud will normally redeploy the app.

## 5. Quick validation checklist

- [ ] App starts with `streamlit run app.py`.
- [ ] PDF, DOCX, and TXT uploads are accepted.
- [ ] Unsupported files and files over 5 MB are rejected.
- [ ] A scanned PDF with no extractable text shows a helpful message.
- [ ] Missing API key shows a configuration message.
- [ ] A valid API key returns a review and download button.
- [ ] Job-description matching is tested with a sample job posting.

## Notes and limitations

- PDF text extraction does not perform OCR; scanned image-only PDFs may not work.
- Gemini API usage is subject to Google's current model availability, quotas, and billing/usage terms.
- Resume content is sent to Google's Gemini API for analysis. Obtain consent and avoid uploading confidential documents without permission.
- This app does not guarantee ATS compatibility, interviews, or hiring outcomes.
