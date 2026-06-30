**JWT Security Analyzer**

_Lightweight JWT Vulnerability Detection & Risk Scoring_

Python | FastAPI | Jinja2 | Pytest | JavaScript

# Preview

Paste JWT → Analyze → Security Report

**Risk Score: 75 / 100**

**Header**

{ "alg": "none" }

**Payload**

{ "password": "123456" }

**Findings**

• alg=none detected

• Missing expiration claim

• Sensitive data in payload

# Features

## JWT Decoding

- Decodes header and payload automatically
- Supports Base64URL decoding
- Displays token structure clearly

## Security Checks

The analyzer detects the following common JWT security issues:

| **Check**                     | **Severity** | **Description**                         |
| ----------------------------- | ------------ | --------------------------------------- |
| alg = none                    | Critical     | Token can be forged without a signature |
| Missing exp                   | Warning      | Token never expires                     |
| Expired token                 | High         | Token already invalid                   |
| Remote key loading (jku, x5u) | High         | Possible SSRF / key confusion           |
| Sensitive payload fields      | Warning      | Payload should not contain secrets      |

## Risk Scoring

Each finding contributes to a risk score (capped at 100):

| **Severity** | **Score** |
| ------------ | --------- |
| critical     | 45        |
| high         | 30        |
| warning      | 15        |
| info         | 5         |

Risk level categories:

| **Score** | **Level** |
| --------- | --------- |
| 0         | Safe      |
| 1 - 39    | Low Risk  |
| 40 - 79   | High Risk |
| 80 - 100  | Critical  |

# Tech Stack

| **Technology** | **Purpose**          |
| -------------- | -------------------- |
| Python         | Backend language     |
| FastAPI        | Web API framework    |
| Jinja2         | HTML templating      |
| Pytest         | Unit testing         |
| JavaScript     | Frontend interaction |

# Installation

## Clone the repository

git clone <https://github.com/YOUR_USERNAME/jwt-security-analyzer.git>

cd jwt-security-analyzer

## Create virtual environment

python3 -m venv .venv

source .venv/bin/activate

## Install dependencies

pip install fastapi uvicorn jinja2 pydantic pytest

# Run the Application

Start the development server:

uvicorn app.main:app --reload

Open in browser:

<http://127.0.0.1:8000>

API documentation:

<http://127.0.0.1:8000/docs>

# Running Tests

Run the unit tests:

pytest

The tests validate:

- Invalid JWT format
- alg=none detection
- Missing expiration claim
- Sensitive payload detection
- Valid token parsing

# API Endpoints

| **Method** | **Endpoint** | **Description**    |
| ---------- | ------------ | ------------------ |
| GET        | /            | Web interface      |
| POST       | /analyze     | Analyze a JWT      |
| GET        | /health      | Health check       |
| GET        | /docs        | FastAPI Swagger UI |

## Example Request

{

"token": "eyJhbGciOiJIUzI1NiJ9..."

}

## Example Response

{

"header": {"alg":"HS256"},

"payload": {"sub":"123"},

"findings": \[\],

"risk_score": 0

}

# Project Structure

jwt-security-analyzer/

|

+-- app/

| +-- main.py

| +-- analyzer.py

| +-- checks.py

|

+-- templates/

| +-- index.html

|

+-- tests/

| +-- test_analyzer.py

|

+-- README.md

+-- requirements.txt

+-- .gitignore

# Security Note

**Warning:** JWT payloads should never contain sensitive information. They are only Base64 encoded and can be easily decoded by anyone. This tool helps developers identify insecure token usage early.

# Roadmap

Planned improvements:

- CLI version
- Docker support
- Export analysis reports (JSON / PDF)
- Additional checks (kid confusion, nbf, iss validation)
- Dark mode UI

# Contributing

Contributions are welcome.

- Fork the repository
- Create a feature branch
- Add tests for new checks
- Submit a pull request

# Live Demo

The application is publicly deployed and accessible online:

**Live:** <https://jwt-security-analyzer.onrender.com>

# License

MIT License.