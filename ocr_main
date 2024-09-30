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
