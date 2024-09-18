# pdf-processing-pipeline
This project implements an advanced pipeline to process PDF documents using OCR (Tesseract), EAST text detection, and OpenAI GPT-3. The pipeline extracts text, refines it, generates summaries, flashcards, and performs Google Image searches based on the extracted content.

## Features
PDF to Image Conversion: Convert PDF pages into images for easier processing.
Text Detection Using EAST: EAST-based text segmentation ensures that text regions are accurately identified.
OCR with Tesseract: Detect and extract text from identified regions.
Text Refinement and Summarization: Refine incomplete text using GPT-3, generate summaries and flashcards.
Image Search: Perform Google image search based on extracted and summarized content.
Optimized for Large Files: Efficient memory handling and chunk-based processing to manage large PDFs.
## Installation
#Requirements
Python 3.8 or higher: Make sure Python is installed on your machine. You can download it from Python.org.

Tesseract OCR: Tesseract is required for text extraction. Follow the steps below to install it.

Windows: Download the Tesseract installer and install it. Add the installation path (e.g., C:\Program Files\Tesseract-OCR) to your system's PATH environment variable.

Linux: Run the following command to install:

bash
 
sudo apt-get install tesseract-ocr
macOS: Run the following command to install:

bash
 
brew install tesseract
Install Required Python Libraries:

Clone the repository and install the dependencies using requirements.txt.

bash
 
git clone https://github.com/avi-nasshh/pdf-processing-pipeline.git
cd pdf-processing-pipeline

# Install dependencies
pip install -r requirements.txt
API Configuration
You'll need the following API keys:

OpenAI API Key for text refinement and generation.
Google Custom Search API Key and Search Engine ID for image search.
You can get these API keys by:

OpenAI: Sign up at OpenAI API.
Google API: Get your API key at Google Cloud Console and set up a custom search engine.
Configuration
The pipeline configuration is handled through a Python dictionary, which includes API keys and paths.

Here’s an example of the config dictionary:

python
 
config = {
    'openai_api_key': 'your_openai_api_key_here',
    'google_api_key': 'your_google_api_key_here',
    'search_engine_id': 'your_search_engine_id_here',
    'pdf_path': '/path/to/your/pdf.pdf',
    'tesseract_cmd': r'C:\Program Files\Tesseract-OCR\tesseract.exe',
    'east_model_path': 'frozen_east_text_detection.pb'
}
How It Works
The class-based design allows you to process any PDF by calling a simple method with a custom configuration.

Class Breakdown
pdf_to_images: Converts PDF pages into images using pdf2image.
preprocess_image: Prepares images for text detection by applying image enhancement techniques.
detect_text_east: Detects regions of text using the EAST model and returns bounding boxes.
ocr_on_text_regions: Applies OCR to the detected text regions and extracts text.
refine_with_keywords_or_fallback: Refines the extracted text using OpenAI GPT-3 or provides a fallback if no meaningful text is found.
generate_summary_and_flashcards: Summarizes the refined text and generates flashcards using GPT-3.
generate_image_search_query: Creates a Google search query for the extracted and summarized text.
fetch_image_urls: Fetches relevant image URLs from Google Custom Search API based on the search query.
process_pdf_pipeline: The main method that combines all the steps, processes the PDF, and returns structured output with text, summaries, flashcards, and image URLs.
# Example Usage

# Go to python

config = {
    'openai_api_key': 'your_openai_api_key_here',
    'google_api_key': 'your_google_api_key_here',
    'search_engine_id': 'your_search_engine_id_here',
    'pdf_path': 'C:/path/to/your/pdf.pdf',
    'tesseract_cmd': r'C:\Program Files\Tesseract-OCR\tesseract.exe',
    'east_model_path': 'frozen_east_text_detection.pb'
}

pipeline = PDFProcessingPipeline(config)
output = pipeline.process_pdf_pipeline()

# Print summary, flashcards, and image URLs from each page
for page in output:
    print(f"--- Page {page['page']} ---")
    print(f"Summary: {page['summary']}")
    print(f"Flashcards: {page['flashcards']}")
    print(f"Search Query: {page['search_query']}")
    print(f"Image URLs: {page['image_urls']}")


## How to Use It
Set up your configuration: Modify the config dictionary with the correct API keys and paths.
Run the pipeline: Execute the script to process your PDF and generate text, summaries, and image searches.
Examine the results: The output will be printed or returned in a structured format.
Future Improvements
Expand to multi-language support by integrating multi-language OCR options.
Add GUI for easier interaction for non-technical users.
Expand to more AI models for specialized medical term extraction.
