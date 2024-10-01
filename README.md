# OCR Web Application using ColPali + Byaldi + Qwen2-VL with Streamlit Deployment

This repository contains an approach towards developing and deploying a web-based prototype that demonstrates the ability to perform Optical Character Recognition (OCR) on an uploaded image (in picture format) containing text in both Hindi and English. It uses the **ColPali implementation of the Byaldi library** and **Huggingface transformers for Qwen2-VL**. The app is developed using **Streamlit** for ease of use and deployment.
The web application also implements a search functionality based on the extracted text. The prototype is accessible via a live URL.

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Prerequisites](#prerequisites)
3. [Environment Setup](#environment-setup)
4. [Running the Web Application Locally](#running-the-web-application-locally)
5. [Deployment](#deployment)
6. [Access the Live App](#access-the-live-app)
7. [Results](#results)
8. [Contributing](#contributing)
9. [License](#license)

---

## Project Overview

This project is an OCR application that allows users to upload images with mixed-language text (English and Hindi). The OCR engine extracts the text, and users can search for keywords within the extracted content.

The project uses:
- **ColPali's Byaldi library** for text extraction.
- **Huggingface Qwen2-VL** model for handling multiple languages.
- **Streamlit** for building a simple and interactive web interface.

---

## Prerequisites

Before setting up the project, make sure you have the following dependencies installed on your machine:
- **Python**
- **pip** (Python package installer)
- A modern web browser to access the web interface
- Refer to below link
  [Requirements](https://github.com/Sakshi-Hardwani/Web_Based_OCR_Application/blob/main/requirements.txt)
  [Packages](https://github.com/Sakshi-Hardwani/Web_Based_OCR_Application/blob/main/packages.txt)

For deployment:
- A **GitHub account** (for hosting code)
- **Streamlit Cloud** (for deployment)

---

## Environment Setup

To set up environment in **local sysytem** install all the dependencies in your system and also give path if required.

To set up the environment for **Streamlit** and install the necessary dependencies, follow these steps:

 **Clone the Repository**:
```
   git clone https://github.com/Sakshi-Hardwani/Web_Based_OCR_Application
```
---


## Running the Web Application Locally
Once the environment is set up and the dependencies are installed, you can run the application locally.

### Saving and Running the Code Locally.

### Step 1: Save the Code in Notepad

1. Open **Notepad** on your system.
2. Copy the following code and paste it into Notepad:

```
import streamlit as st
from PIL import Image
import pytesseract
import re

# Title of the application
st.title("OCR Text Extraction and Search")

# File uploader for images
uploaded_file = st.file_uploader("Choose an image...", type=["jpg", "jpeg", "png"])

# If an image is uploaded
if uploaded_file is not None:
    # Open the image file
    image = Image.open(uploaded_file)
    
    # Display the image
    st.image(image, caption="Uploaded Image", use_column_width=True)

    # Perform OCR on the uploaded image, specify both English and Hindi languages
    extracted_text = pytesseract.image_to_string(image, lang='eng+hin')
    
    # Display the extracted text
    st.subheader("Extracted Text:")
    st.write(extracted_text)
    
    # Input for search functionality (can include both English and Hindi terms separated by commas)
    search_terms = st.text_input("Enter words or phrases to search for (supports both English and Hindi, separated by commas):")

    # Highlight search terms in the extracted text with neon green using HTML/Markdown
    if search_terms:
        # Function to highlight multiple search terms in neon green
        def highlight_terms(text, terms):
            # Split the input terms by comma to get a list of terms
            terms = [term.strip() for term in terms.split(',')]
            
            # Iterate over each term and highlight them in the text
            for term in terms:
                pattern = re.compile(re.escape(term), re.IGNORECASE)  # Use case-insensitive matching
                text = pattern.sub(f'<span style="background-color: #39ff14; color: black;"><b>{term}</b></span>', text)
            
            return text

        # Highlight the search terms (can be both Hindi and English) in the extracted text
        highlighted_text = highlight_terms(extracted_text, search_terms)
        
        st.subheader("Highlighted Text (Markdown Output):")
        # Display the highlighted text with HTML/Markdown
        st.markdown(highlighted_text, unsafe_allow_html=True)

# Instructions for the user
st.markdown("""
### Instructions:
1. Upload an image containing text in English or Hindi.
2. The application will extract the text from the image.
3. Enter multiple words or phrases in either English or Hindi (separate them using commas) to search for in the extracted text.
4. The matching terms will be highlighted in neon green in the markdown output.
""")
```
### Step 2: Save the file with a .py extension:
- Click on File > Save As.
- In the File Name field, enter ocr_main.py.
- In the Save as type dropdown, select All Files.
- Choose a folder where you want to save the file, and click Save.

### Step 3: Navigate to the Folder in Command Prompt
Open Command Prompt on your computer.
Use the cd (change directory) command to navigate to the folder where you saved the ocr_main.py file. For example:
```
cd C:\Users\YourUsername\Documents\OCR_Project
```
Make sure to replace C:\Users\YourUsername\Documents\OCR_Project with the actual path where your Python file is saved.

### Step 4: Run the Application Locally Using Streamlit
Once you’re in the correct folder, run the application using Streamlit by typing the following command: For example:
```
python -m streamlit run ocr_main.py
```
This will start the Streamlit server, and you will see output in the terminal like:

![Command Prompt](https://github.com/Sakshi-Hardwani/Web_Based_OCR_Application/blob/main/localhost_ocr_streamlit.png)

You can now view your Streamlit app in your browser.
Open your browser and go to http://localhost:8501 to access the OCR web application running locally on your machine.

![Local Host Streamlit](https://github.com/Sakshi-Hardwani/Web_Based_OCR_Application/blob/main/streamlit_interface.png)

---
## Deployment
After testing if the application runs smoothly deploy it using **Streamlit**

### Streamlit Cloud Deployment

### Step 1: Sign Up for Streamlit Cloud
- [Streamlit Cloud](https://share.streamlit.io/)

### Step 2: Push Your Repository to GitHub
- Make sure your application code is pushed to a GitHub repository.

### Step 3: Deploy on Streamlit Cloud
1. Log in to [Streamlit Cloud](https://share.streamlit.io/).
2. Create a new app and link it to your GitHub repository.
   - Navigate to Create App -> Yes I have an App -> Fill Info -> Deploy
4. Streamlit will automatically build and deploy your app. 
---

## Access the Live App
- After deployment, you’ll receive a live URL that you can share with others to access the app online.
- Example
  - [Live URL](https://web-application-based-ocr.streamlit.app/)
---

## Results

Below are some example images of web applications interface and working.

Image Used

![Image Used](https://github.com/Sakshi-Hardwani/Web_Based_OCR_Application/blob/main/hindi-english.jpg) 

Streamlit OCR Deployed Version

![Streamlit OCR Deployed Version](https://github.com/Sakshi-Hardwani/Web_Based_OCR_Application/blob/main/streamlit_cloud_deployed_interface_with_url.png)

Image File Upload

![Image File Upload](https://github.com/Sakshi-Hardwani/Web_Based_OCR_Application/blob/main/file_upload_output.png)

Extrcated Text

![Extrcated Text](https://github.com/Sakshi-Hardwani/Web_Based_OCR_Application/blob/main/extracted_text_output.png)

Search Functionality

![Search Functionality](https://github.com/Sakshi-Hardwani/Web_Based_OCR_Application/blob/main/search_functionality_output.png)

---

## Contributing

### Contributions are welcome! 

To contribute:
- Fork this repository.
- Create a feature branch (git checkout -b feature/your-feature).
- Commit your changes (git commit -m 'Add your feature').
- Push to the branch (git push origin feature/your-feature).
- Open a pull request.

---

## License

---
   
