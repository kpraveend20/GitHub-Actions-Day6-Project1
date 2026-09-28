Day 6 Project 1 — Production-Style GitHub Actions CI
📌 Project Overview

This project demonstrates a production-style Continuous Integration (CI) pipeline using GitHub Actions.

The workflow automatically validates the Python application when:

A Pull Request is created against main
Code is pushed to main
The workflow is manually triggered using workflow_dispatch

The pipeline performs Python syntax validation, installs dependencies, runs automated tests, and checks that the Dockerfile exists.

🎯 Project Objective

The main objective of this project is to understand how GitHub Actions can automatically validate code before it is merged into the main branch.

The CI flow is:

Developer
    |
    v
Feature Branch
    |
    v
Pull Request
    |
    v
GitHub Actions
    |
    +----> Checkout Code
    |
    +----> Setup Python
    |
    +----> Install Dependencies
    |
    +----> Python Syntax Check
    |
    +----> Run Pytest
    |
    +----> Check Dockerfile
    |
    v
CI SUCCESS
    |
    v
Merge to main
🛠️ Technologies Used
Git
GitHub
GitHub Actions
Python 3.12
Pytest
Docker
YAML
📂 Project Structure
GitHub-Actions-Day6-Project1/
│
├── app.py
├── requirements.txt
├── test_app.py
├── Dockerfile
├── README.md
│
└── .github/
    └── workflows/
        └── ci.yml
File Description
File	Purpose
app.py	Python application
test_app.py	Automated tests
requirements.txt	Python dependencies
Dockerfile	Docker image definition
.github/workflows/ci.yml	GitHub Actions CI workflow
README.md	Project documentation
🔄 GitHub Actions Workflow

The workflow is located at:

.github/workflows/ci.yml

The workflow has three triggers.

1. Pull Request Trigger
on:
  pull_request:
    branches:
      - main

This runs the CI pipeline when a Pull Request targets the main branch.

Purpose:

Pull Request
     |
     v
CI Checks
     |
     v
Tests Passed?
     |
     +---- Yes ---> Ready for review/merge
     |
     +---- No ----> Fix code

This helps identify problems before code is merged into main.

2. Push to Main
push:
  branches:
    - main

This runs the workflow when code is pushed to the main branch.

Typical flow:

Feature Branch
      |
      v
Pull Request
      |
      v
Review
      |
      v
Merge
      |
      v
main
      |
      v
GitHub Actions
3. Manual Workflow
workflow_dispatch:

This allows the workflow to be manually started from the GitHub Actions page.

Path:

GitHub Repository
        ↓
Actions
        ↓
Day 6 CI Pipeline
        ↓
Run workflow

Manual execution is useful for testing and troubleshooting workflows.

⚙️ CI Pipeline Steps

The workflow performs the following steps.

Step 1 — Checkout Code
- name: Checkout code
  uses: actions/checkout@v4

This downloads the repository code into the GitHub Actions runner.

Step 2 — Setup Python
- name: Setup Python
  uses: actions/setup-python@v5
  with:
    python-version: "3.12"

This installs and configures Python 3.12 on the GitHub-hosted runner.

Step 3 — Install Dependencies
- name: Install dependencies
  run: |
    python -m pip install --upgrade pip
    pip install -r requirements.txt

This installs the Python packages required by the application.

In this project:

pytest

is installed.

Step 4 — Python Syntax Check
- name: Python syntax check
  run: |
    python -m py_compile app.py
    python -m py_compile test_app.py

This checks whether the Python files contain syntax errors.

If the syntax is invalid, the workflow fails.

Step 5 — Run Tests
- name: Run tests
  run: |
    pytest -v

Pytest executes the automated tests from test_app.py.

Expected result:

2 passed
Step 6 — Check Dockerfile
- name: Check Dockerfile
  run: |
    test -f Dockerfile
    echo "Dockerfile exists"

This verifies that the Dockerfile exists in the repository.

🐍 Python Application

The application contains two simple functions:

def add(a, b):
    return a + b


def multiply(a, b):
    return a * b

The tests verify:

10 + 20 = 30
10 × 20 = 200
🧪 Local Testing

Before pushing the project to GitHub, the application can be tested locally.

Run the application
python app.py

Expected output:

Day 6 CI/CD Demo Application
Addition: 30
Multiplication: 200
Install pytest
python -m pip install pytest
Run tests
python -m pytest

Expected result:

2 passed
🐳 Docker

The project also contains a basic Dockerfile.

Build the Docker image:

docker build -t day6-ci-demo .

Check the image:

docker images

Run the container:

docker run --rm day6-ci-demo

Expected output:

Day 6 CI/CD Demo Application
Addition: 30
Multiplication: 200
🔐 GitHub Actions Permissions

The workflow uses:

permissions:
  contents: read

This gives the workflow read access to repository contents.

For this CI-only project, no AWS credentials or AWS permissions are required.

📊 CI Workflow Summary
                GitHub Repository
                       |
                       v
                 Pull Request
                       |
                       v
               GitHub Actions
                       |
              +--------+--------+
              |        |        |
              v        v        v
          Checkout   Python   Dependencies
                       |
                       v
                 Syntax Check
                       |
                       v
                    Pytest
                       |
                       v
                 Dockerfile
                    Check
                       |
                       v
                    SUCCESS
🔑 Important Concepts Learned
Continuous Integration

CI automatically checks code whenever developers make changes.

Pull Request

A Pull Request allows code changes to be reviewed and validated before merging.

GitHub Actions

GitHub Actions automates CI/CD tasks using workflow files written in YAML.

Workflow Trigger

Triggers determine when a GitHub Actions workflow starts.

Examples:

pull_request
push
workflow_dispatch
Automated Testing

Automated tests verify that application functionality is working correctly.

GitHub Actions Runner

The workflow executes on a GitHub-hosted runner such as:

ubuntu-latest
🚀 Git Workflow Used

The project follows a basic feature branch workflow:

main
 |
 +---- feature-update
            |
            v
       Code Changes
            |
            v
       Pull Request
            |
            v
     GitHub Actions CI
            |
            v
          PASS
            |
            v
       Merge to main
📸 GitHub Actions Result

After pushing the project to GitHub:

Go to:

Repository
    ↓
Actions
    ↓
Day 6 CI Pipeline

The workflow should show a successful run.

Expected steps:

✓ Checkout code
✓ Setup Python
✓ Install dependencies
✓ Python syntax check
✓ Run tests
✓ Check Dockerfile
✓ CI completed


🎓 Interview Explanation
Q1. What did you build in this project?

I built a GitHub Actions Continuous Integration pipeline that automatically validates a Python application.

Q2. When does the workflow run?

It runs on Pull Requests targeting main, pushes to main, and manual workflow_dispatch executions.

Q3. What checks are performed?

The workflow performs Python syntax validation, dependency installation, automated pytest execution, and Dockerfile validation.

Q4. Why use Pull Request CI?

Pull Request CI helps identify code problems before changes are merged into the main branch.

Q5. Why use automated tests?

Automated tests provide a repeatable way to verify that application functionality continues to work after code changes.

Q6. What is workflow_dispatch?

workflow_dispatch allows a GitHub Actions workflow to be manually started from the GitHub Actions interface.

Q7. What is the next step after this CI project?

The next step is to build a Docker image, authenticate to AWS using GitHub Actions OIDC, and push the image to Amazon ECR.

📈 Day 6 Learning Progress
Day 1
GitHub Actions Basics
        ↓
Day 2
Git Checkout + Shell
        ↓
Day 3
Jenkins + GitHub
        ↓
Day 4
Triggers + Secrets
        ↓
Day 5
Docker + GitHub Actions + ECR
        ↓
Day 6 Project 1
Production-Style CI
        ↓
Day 6 Project 2
GitHub Actions → Docker → ECR
        ↓
Future
Staging → Approval → Production
✅ Project Status

Python application created

Unit tests created

Dockerfile created

GitHub Actions workflow created

Pull Request trigger configured

Push to main trigger configured

Manual workflow trigger configured

Python syntax check configured

Pytest configured

Dockerfile validation configured

Push project to GitHub

Create feature branch

Create Pull Request

Verify GitHub Actions CI

Merge Pull Request

👨‍💻 Author

Praveen D

Learning GitHub Actions, Docker, AWS and DevOps CI/CD.