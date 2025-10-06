# Personal Injury Demand Letter Generator

## Project Overview
Build a California personal injury demand letter automation system for a law firm. This application will manage medical records, prevent duplicates, and generate professional demand letters using Claude API with full case context.

## Tech Stack
- **Backend**: Python 3.11+ with FastAPI
- **Database**: PostgreSQL with pgvector extension  
- **AI**: Anthropic Claude API (claude-sonnet-4-5-20250929)
- **Document Processing**: python-docx, pdfplumber, PyPDF2
- **Caching**: Redis for file deduplication

## Key Requirements

### 1. File Deduplication
- Use SHA-256 hashing to prevent duplicate file uploads
- Store hashes in Redis with metadata
- Reject duplicates with clear error messages

### 2. Medical Record Management
- Parse PDF medical records to extract: provider, dates, diagnoses, charges
- Store in PostgreSQL with full text and structured data
- Track relationships between records and case

### 3. Demand Letter Generation  
- Use Claude API to generate complete demand letters
- Provide FULL case context (all medical records) in each API call
- Support regeneration of sections or entire letter
- Track which medical records are cited in each section

## Project Structure Needed
src/
├── main.py                 # FastAPI application
├── core/
│   ├── config.py          # Settings
│   └── database.py        # DB connection
├── models/
│   ├── case.py            # Case data model
│   ├── medical_record.py  # Medical record model
│   └── demand_letter.py   # Letter model
├── services/
│   ├── file_manager.py    # Upload & deduplication
│   ├── medical_parser.py  # Parse PDFs
│   └── ai_generator.py    # Claude API integration
└── api/
└── routes/
├── cases.py
├── medical_records.py
└── demand_letters.py

## Environment Variables Needed
```env
ANTHROPIC_API_KEY=your_key_here
DATABASE_URL=postgresql://user:pass@localhost:5432/demand_letters
REDIS_URL=redis://localhost:6379
Development Priority

Phase 1: Project structure, dependencies (pyproject.toml), database models
Phase 2: File upload system with SHA-256 deduplication
Phase 3: Medical record PDF parser
Phase 4: Claude API integration for letter generation
Phase 5: API endpoints and testing

Critical Success Factors

No Duplicate Files: SHA-256 hash checking before accepting uploads
Full Context: Every Claude API call must include ALL medical records for the case
Citation Tracking: Know which medical records support each claim in letter
Clean Architecture: Separate concerns (file handling, parsing, AI generation)

Getting Started
Create the basic project structure, set up FastAPI, configure database models, and implement file deduplication first.
