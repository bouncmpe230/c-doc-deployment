# C Documentation and Deployment

This repository includes an example for automating C documentation and deploying it to GitHub Pages.

## **Overview**
This project demonstrates how to:
- Use **Doxygen** to generate documentation from C code.
- Automate documentation generation with **GitHub Actions**.
- Deploy the generated documentation to **GitHub Pages**.

## **Setup and Usage**
### **1. Install Doxygen**
Before running the documentation generation, install **Doxygen**:
- **Linux (Debian/Ubuntu):** `sudo apt install doxygen`
- **macOS:** `brew install doxygen`
- **Windows:** Download from [Doxygen official site](https://www.doxygen.nl/)

### **2. Configure Doxygen**
Generate a default `Doxyfile`:
```sh
doxygen -g Doxyfile
```
Modify `Doxyfile` to include:
```
OUTPUT_DIRECTORY = docs
GENERATE_HTML = YES
EXTRACT_ALL = YES
INPUT = src/
RECURSIVE = YES
FILE_PATTERNS = *.c *.h
```
Run Doxygen to generate documentation:
```sh
doxygen Doxyfile
```

### **3. Automate Deployment with GitHub Actions**
GitHub Actions is set up to generate documentation and deploy it to **GitHub Pages** whenever changes are pushed.

The workflow file `.github/workflows/doxygen.yml` includes:
```yaml
name: Generate Doxygen Documentation

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repository
      uses: actions/checkout@v3

    - name: Install Doxygen
      run: sudo apt-get install doxygen -y

    - name: Generate Documentation
      run: doxygen Doxyfile

    - name: Deploy to GitHub Pages
      uses: JamesIves/github-pages-deploy-action@v4
      with:
        branch: gh-pages
        folder: docs/html
        token: ${{ secrets.GITHUB_TOKEN }}
```

### **4. Enable GitHub Pages**
- Go to **Settings → Pages** in your repository.
- Under **Source**, select **Deploy from branch**.
- Set the branch to `gh-pages` and the folder to `/ (root)`.
- Click **Save**.

### **5. Access Documentation**
Once deployed, your documentation will be available at:
```
https://yourusername.github.io/c-doc-deployment/
```

## **Contributing**
Feel free to submit pull requests for improvements or bug fixes.

## **License**
This project is open-source and available under the MIT License.

