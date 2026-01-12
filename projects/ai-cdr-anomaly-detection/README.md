# AI-Powered Anomaly Detection System (Closed-Source Project)

## Snapshot

- Type: Proof-of-Concept (POC) - AI-based operational data analysis
- My role: Full-stack developer (design, implementation, testing)
- Users / Stakeholders: Operations teams analyzing call detail records (CDR) data
- Status: Production POC at Wasabi

## Problem

- Manual rule-based anomaly detection required constant maintenance as patterns evolved
- Complex relationships in operational data were difficult to capture with static rules
- Unknown anomaly patterns went undetected until they caused issues
- Analysis workflows were time-consuming and required domain expertise

## Solution

- Built a pure AI-based detection system that automatically identifies anomalies in CDR data without predefined rules
- Implemented intelligent data sampling and formatting to optimize AI analysis costs
- Created a web interface with categorized anomaly reports (errors, performance, rate limiting, etc.)
- Added interactive Q&A feature allowing users to query the AI about detected patterns

## What I owned

- Designed and implemented the full-stack architecture (Next.js frontend + API routes)
- Built the AI detection engine with smart data formatting and prompt engineering
- Created data normalization pipeline for CSV uploads with field name standardization
- Implemented result parsing and categorization into 7 anomaly types
- Developed interactive UI with tabbed views for different anomaly categories
- Optimized for cost and performance with automatic data sampling for large datasets

## How it works (high-level)

Users upload CSV files containing CDR data through a web interface. The system normalizes field names and stores data in frontend state. When analysis is triggered, the backend formats the data into statistical summaries and raw records, then sends a structured prompt to the OpenAI API. The AI analyzes the data and returns JSON-formatted results with categorized anomalies, reasoning, and confidence scores. The frontend parses and displays results across 9 specialized tabs (Summary, Errors, Performance, Rate Limiting, Redirects, Egress Spikes, Authentication Issues, Service Failures, and AI Q&A).

## Tech stack

- Next.js (App Router)
- TypeScript
- OpenAI API
- React components
- CSV parsing and data normalization

## Results / Impact

- Eliminated need for rule maintenance by using adaptive AI detection
- Reduced analysis time from manual review to automated 5-10 second processing
- Enabled discovery of previously unknown anomaly patterns through semantic analysis
- Cost-optimized to approximately $0.01-0.10 per analysis depending on dataset size

## Challenges & Tradeoffs

- **Cost vs. Accuracy**: Implemented smart sampling for large datasets to balance AI API costs while maintaining detection quality
- **Consistency vs. Flexibility**: Used temperature=0.3 to reduce variability while preserving AI's ability to discover novel patterns
- **Data Volume**: Designed automatic sampling strategy to handle datasets exceeding API token limits without losing representative insights
- **User Experience**: Added progress indicators and structured result presentation to make AI reasoning transparent and actionable
- **Production Readiness**: Built as POC to validate approach; production deployment would require additional error handling, rate limiting, and result caching

## Confidentiality note

This project was developed as a production proof-of-concept at Wasabi for operational data analysis. Code, API endpoints, and proprietary data schemas are not included. I'm happy to walk through the architecture, design decisions, and technical implementation in detail during interviews.

