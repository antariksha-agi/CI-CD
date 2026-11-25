# CI-CD
Yep. Let's create a reusable Python CI template that you can copy into most future Python projects, including FastAPI, AI agents, RAG pipelines, and backend services.

This is a better starter than our first workflow because it includes dependency installation, testing, linting, and runs on both pushes and pull requests.
1. Your reusable Python CI template
Create this file in every Python project's repository:
.github/workflows/ci.yml


Paste this template:

name: Python CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  quality:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v7

      - name: Set up Python
        uses: actions/setup-python@v7
        with:
          python-version: "3.12"
          cache: pip

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Lint with Ruff
        run: |
          pip install ruff
          ruff check .

      - name: Run tests
        run: |
          python -m pytest -v



I've used the current major versions of the official checkout and setup-python actions. 
GitHub+1


2. What you need in each project
Your Python project should generally have:
my-project/
├── .github/
│   └── workflows/
│       └── ci.yml
├── app/
├── tests/
├── requirements.txt
└── .gitignore


Your requirements.txt should include your project dependencies and test dependencies, such as:
fastapi
pytest


Ruff is installed separately in the workflow, so you don't have to put it in your application's requirements file.

3. What this template automatically does
When	What happens
Push to main	CI runs
Pull request into main	CI runs
Dependencies install	Environment is prepared
Ruff runs	Checks for common Python mistakes and style issues
pytest runs	Executes your automated tests
Any check fails	Workflow turns red ❌
All checks pass	Workflow turns green ✅


4. How to reuse it
When starting a new Python project:
1. Create .github/workflows/.
2. Copy ci.yml into it.
3. Change Python version if required.
4. Make sure your requirements.txt exists.
5. Make sure your tests can run with pytest.
6. Push to GitHub.
For FastAPI, agents, RAG projects and Python backends, this is a good starting CI template. Larger projects will eventually need database integration tests, security checks, type checking, Docker builds and evaluation pipelines—but don't add complexity until the project needs it.

This is your starter CI template. Save it; you don't need to reinvent the workflow every time. 😎
