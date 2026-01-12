# AI Job Description Matcher (Closed-Source Portfolio)

## Snapshot

- Type: AI-powered matching tool
- My role: Full-stack developer (backend, AI integration, frontend)
- Users / Stakeholders: HR and recruitment teams matching internal and external job descriptions
- Status: Completed project

## Problem

- Manual comparison of job descriptions was time-consuming and inconsistent
- Keyword-based matching missed semantic similarities and contextual nuances
- Needed to process multiple file formats (CSV, Excel, Word, plain text)
- Required scalable solution that could handle batch processing of job descriptions

## Solution

- Built a semantic similarity matching system using sentence-BERT embeddings
- Created a web interface supporting multiple file formats with automatic format detection
- Implemented asynchronous file processing to handle large batches without blocking
- Designed intuitive UI with automatic result download upon completion

## What I owned

- Designed and implemented the FastAPI backend with file upload and matching endpoints
- Integrated sentence-BERT model for semantic similarity calculations
- Built file parsing logic supporting CSV, XLSX, DOCX, and TXT formats with flexible column name matching
- Created frontend interface with Bootstrap styling and JavaScript for async processing
- Implemented automatic file download functionality for matched results
- Handled edge cases for different file formats (single-document files vs. multi-row spreadsheets)

## How it works (high-level)

Users upload two files through a web interface: one containing internal job descriptions and another with external job descriptions. The backend parses files based on format, extracting job IDs and descriptions using flexible column name matching. For each internal job description, the system generates sentence embeddings using a pre-trained sentence-BERT model. It then computes cosine similarity scores against all external job descriptions. The top matches are ranked by similarity score and compiled into a results file. The frontend displays progress during processing and automatically triggers download of the matched results upon completion.

## Tech stack

- FastAPI (Python web framework)
- Sentence Transformers (sentence-BERT)
- pandas (data processing)
- python-docx (Word document parsing)
- HTML/CSS/JavaScript (frontend)
- Bootstrap (UI framework)

## Results / Impact

- Automated semantic matching eliminated manual comparison workflows
- Improved matching accuracy by capturing contextual similarities beyond keyword overlap
- Reduced processing time for batch job description comparisons
- Supported multiple file formats, increasing usability across different data sources

## Challenges & Tradeoffs

- **Performance vs. Accuracy**: Used sentence-BERT for good balance between speed and semantic understanding, accepting that transformer models require more compute than simple keyword matching
- **Flexibility vs. Structure**: Implemented flexible column name matching to handle various file formats, requiring robust parsing logic
- **Synchronous vs. Asynchronous**: Chose async file processing to handle large batches, requiring progress indicators and result download mechanisms
- **Model Selection**: Selected sentence-BERT over larger language models to balance accuracy with inference speed and resource requirements
- **File Format Complexity**: Supported multiple formats increased development complexity but improved user experience and adoption

## Confidentiality note

This project was developed for internal HR use. Source code, model configurations, and proprietary data schemas are not included. I'm available to discuss the semantic matching approach, file processing architecture, and technical implementation details in interviews.

