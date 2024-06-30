### Project Description

**Text Summarizer: Efficient Text and Document Summarization**

Text Summarizer is a powerful application designed to help users efficiently condense large texts and documents into concise summaries. Built with Streamlit for an interactive interface, this tool leverages the txtai library for natural language processing and PyPDF2 for extracting text from PDF documents. Whether you're summarizing typed text or uploaded PDF files, Text Summarizer aims to enhance your reading and comprehension experience by providing quick and accurate summaries.

### README

# Text Summarizer: Efficient Text and Document Summarization

## Overview

Text Summarizer is a Streamlit-based application that provides users with the ability to summarize large blocks of text and PDF documents. It uses the txtai library to generate summaries and PyPDF2 to extract text from PDF files.

## Features

- **Summarize Text**: Input any block of text and get a concise summary.
- **Summarize Document**: Upload a PDF file and receive a summary of its content.
- **Interactive UI**: Easy-to-use interface powered by Streamlit.
- **Efficient Processing**: Quick and accurate text extraction and summarization.

## Installation

1. Clone the repository:

```bash
git clone https://github.com/dearcoder03/Wifi-Password-Viewer.git
cd Text-Summarizer
```

2. Install the required dependencies:

```bash
pip install streamlit txtai PyPDF2
```

3. Run the application:

```bash
streamlit run app.py
```

## Usage

1. **Summarize Text**:
   - Select "Summarize Text" from the sidebar.
   - Enter your text in the provided text area.
   - Click the "Summarize Text" button to generate a summary.

2. **Summarize Document**:
   - Select "Summarize Document" from the sidebar.
   - Upload a PDF file using the file uploader.
   - Click the "Summarize Document" button to extract text and generate a summary.

## Code Explanation

### Main Application (`app.py`)

```python
import streamlit as st
from txtai.pipeline import Summary
from PyPDF2 import PdfReader

st.set_page_config(layout="wide")

@st.cache_resource
def text_summary(text, maxlength=None):
    summary = Summary()
    result = summary(text)
    return result

def extract_text_from_pdf(file_path):
    with open(file_path, "rb") as f:
        reader = PdfReader(f)
        page = reader.pages[0]
        text = page.extract_text()
    return text

st.header('📝 Text Summarizer')

choice = st.sidebar.selectbox("Select your choice", ["Summarize Text", "Summarize Document"])

if choice == "Summarize Text":
    st.subheader("Summarize Text")
    input_text = st.text_area("Enter your text here")
    if input_text:
        if st.button("Summarize Text"):
            col1, col2 = st.columns([1, 1])
            with col1:
                st.markdown("**Your Input Text**")
                st.info(input_text)
            with col2:
                st.markdown("**Summary Result**")
                result = text_summary(input_text)
                st.success(result)

elif choice == "Summarize Document":
    st.subheader("Summarize Document using txtai")
    input_file = st.file_uploader("Upload your document here", type=['pdf'])
    if input_file:
        if st.button("Summarize Document"):
            with open("doc_file.pdf", "wb") as f:
                f.write(input_file.getbuffer())
            col1, col2 = st.columns([1, 1])
            with col1:
                st.info("File uploaded successfully")
                extracted_text = extract_text_from_pdf("doc_file.pdf")
                st.markdown("**Extracted Text is Below:**")
                st.info(extracted_text)
            with col2:
                st.markdown("**Summary Result**")
                text = extract_text_from_pdf("doc_file.pdf")
                doc_summary = text_summary(text)
                st.success(doc_summary)
```

## Contribution

Contributions are welcome! Feel free to submit a pull request or open an issue for any feature requests or bugs.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

Enjoy using Text Summarizer!
