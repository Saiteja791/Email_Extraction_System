## Email Job Extractor

Email Job Extractor is a Python + Streamlit application that connects to an IMAP inbox, automatically fetches job-related emails, extracts structured job information using NLP, and stores the results in an Excel file with a built-in analytics dashboard.

## Features

- **Automated email ingestion**: Connects to IMAP providers (Gmail, Outlook, Yahoo, etc.) and supports unread-only and date-range based extraction.
- **NLP-powered extraction**: Uses BERT NER (Hugging Face), with spaCy/TextBlob/regex fallbacks, to extract job title, company, location, skills, experience, salary, deadlines, and summaries from unstructured email text.
- **Deduplication**: Tracks each email by its `Message-ID` to avoid re-processing and duplicate rows across multiple runs.
- **Timezone-aware date ranges**: Precise date filtering using timezone-safe UTC conversions and clear reporting of skipped emails (out of range / parse errors).
- **Interactive dashboard**: Streamlit UI with KPIs, charts, advanced filters, and CSV/Excel export for downstream analysis.
- **Per-account storage**: Separate Excel file per email account to keep data clean and isolated.

## Tech Stack

- **Backend / App**: Python, Streamlit  
- **Email**: `imaplib`, IMAP over SSL  
- **NLP**: Transformers (BERT NER `dslim/bert-base-NER`), spaCy, TextBlob, NLTK, regex  
- **Data & Storage**: Pandas, OpenPyXL (Excel)  
- **Utilities**: python-dotenv, BeautifulSoup, dateutil, pytz, tzlocal, schedule, Plotly

## Project Structure

- **`app.py`**: Main Streamlit app and UI (sidebar config, tabs, dashboard, results, settings).
- **`email_client.py`**: IMAP client for connecting, fetching unread emails, and date-range queries with robust date parsing.
- **`text_processor.py` / `text_processor_improved.py`**: NLP pipeline for cleaning email text and extracting job-related fields.
- **`excel_manager.py`**: Excel file management, Message-ID based deduplication, search and export utilities.
- **`config.py`**: Central configuration and `.env` loading.
- **`run_app.bat`**: Windows helper script to start the Streamlit app.

## Accuracy (Internal Evaluation)

- **Overall field-level extraction accuracy**: ~82% (average across title, company, location, skills, salary).  
- **Per-field (approximate)**: ~85% job title, ~90% company, ~80% location accuracy on manually labelled samples.

> Note: These are internal evaluation numbers on a limited labeled set; real-world performance depends on email formats and domains.

## Getting Started

### 1. Clone the repository

git clone <your-repo-url>.git
cd EMAILS_EXT
