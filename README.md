# .github/workflows/python-ci.yml
name: 🧪 Python CI Workflow

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
    - name: 📥 Checkout code
      uses: actions/checkout@v3

    - name: 🐍 Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.11'

    - name: 📦 Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: 🔍 Lint with flake8
      run: |
        pip install flake8
        flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics

    - name: 🧪 Run tests with pytest
      run: |
        pip install pytest
        pytest

