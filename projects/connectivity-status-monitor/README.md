# Connectivity Status Monitor (Closed-Source Portfolio)

## Snapshot

- Type: Infrastructure monitoring tool
- My role: Full-stack developer and DevOps engineer (architecture, implementation, deployment)
- Users / Stakeholders: Operations teams monitoring endpoint connectivity across regions
- Status: Production deployment

## Problem

- Need to monitor endpoint connectivity (DNS, network reachability, SSL validation) across multiple regions
- Existing monitoring solutions were either too complex or lacked the required customization
- Required minimal infrastructure overhead with no database dependencies
- Needed secure, scalable architecture with least-privilege access controls

## Solution

- Built a decoupled two-component system: a lightweight collector service and a static web dashboard
- Integrated with Uptime.com API to leverage existing monitoring infrastructure instead of custom probes
- Designed S3-compatible object storage (Wasabi) as the data exchange layer, eliminating database requirements
- Implemented secure IAM policies and CORS configuration for public read access with controlled write permissions

## What I owned

- Designed the decoupled architecture separating collector and web frontend
- Implemented the Node.js collector service that fetches data from Uptime.com API and writes unified JSON to S3
- Built the static web dashboard that reads from S3 and renders connectivity status grouped by region
- Configured IAM policies with least-privilege principles for S3 bucket access
- Set up CORS policies for secure cross-origin access
- Created Docker containerization and systemd service configurations for collector deployment
- Implemented Nginx configuration with security headers and SSL/TLS for web interface
- Documented deployment procedures for both Docker and manual setups

## How it works (high-level)

The collector service runs as a scheduled job (systemd timer or Docker container) that periodically fetches check status and metrics from the Uptime.com API. It processes and normalizes the data, then uploads a unified `uptime.json` file to an S3-compatible Wasabi bucket. The static web frontend, deployed independently (Netlify, Vercel, or traditional web server), reads this JSON file directly from the S3 bucket via CORS-enabled GET requests. The frontend parses the data and renders a dashboard showing connectivity status, latency metrics, SSL certificate information, and regional groupings. No database or backend server is required—the S3 bucket serves as both storage and cache.

## Tech stack

- Node.js
- S3-compatible object storage (Wasabi)
- Uptime.com API
- Docker / Docker Compose
- Systemd timers
- Static HTML/JavaScript frontend
- Nginx (optional web server)

## Results / Impact

- Reduced infrastructure complexity by eliminating database dependencies
- Enabled independent scaling and deployment of collector and web components
- Provided real-time visibility into endpoint connectivity across regions
- Implemented security best practices with least-privilege IAM and controlled public access

## Challenges & Tradeoffs

- **Decoupling vs. Consistency**: Chose S3 as shared storage to enable independent deployment, accepting eventual consistency over real-time synchronization
- **Security vs. Accessibility**: Implemented public read access for static frontend while restricting write operations through IAM policies
- **Simplicity vs. Features**: Prioritized lightweight architecture over advanced features like historical trending or alerting
- **Cost vs. Reliability**: Used object storage instead of database to reduce costs, accepting that data freshness depends on collector schedule
- **Static vs. Dynamic**: Chose static frontend for simplicity and scalability, requiring full page refresh to see updated data

## Confidentiality note

This project was developed for internal infrastructure monitoring. Specific endpoint URLs, bucket names, IAM credentials, and deployment configurations are not included. I can provide detailed walkthroughs of the architecture, security model, and deployment strategies during interviews.

