# AI Experts Assignment (Python)

This repository contains the solution for the AI Software Engineer Assignment.

## Project Overview

The goal of this assignment is to:

- Set up a small Python project that runs reliably locally and in Docker.
- Pin dependencies for reproducible installs.
- Identify and fix a bug in the code.
- Write focused tests and implement a minimal, reviewable fix.

---

## Requirements

- Python 3.11+
- Docker (optional for running tests in container)
- pip (Python package manager)

---

## How to Run Tests Locally

Open a terminal in the project folder and run the following commands:

```bash
# Create and activate virtual environment
python -m venv venv
venv\Scripts\activate      # Windows
# source venv/bin/activate # Mac/Linux

# Install dependencies
pip install -r requirements.txt

# Run tests
pytest -v


## How to Build and Run Tests with Docker

Open a terminal in the project folder and run the following commands:

```bash
# Build the Docker image
docker build -t ai-client .

# Run tests inside the Docker container
docker run --rm ai-client
