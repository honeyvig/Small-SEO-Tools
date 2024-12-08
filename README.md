# Small-SEO-Tools

Plagiarism Checker
Paraphrasing Tool
AI Detector
Free Grammar Checker
Reverse Image Search
Logo Maker
What is My IP
PDF To Word
Internet Speed Test
Website SEO Score Checker
Emojis
Citation Generator
AI Humanizer 
===========
Creating a Python script that combines the functionality for multiple tools like a Plagiarism Checker, Paraphrasing Tool, AI Detector, Free Grammar Checker, Reverse Image Search, Logo Maker, and others can be complex but feasible by integrating several Python libraries and APIs. Below is an example of how one might approach creating such a script. The functionality for each tool will need to be modular, and we'll utilize relevant APIs or Python packages to perform the tasks.

Keep in mind that for certain tools (such as plagiarism checkers, AI detectors, reverse image search, and others), you may need to integrate third-party APIs, as Python doesn't have built-in functionality for everything. Here's an outline and code for this multi-tool script:

import requests
import json
import os
from datetime import datetime
import socket
import pyperclip
from googlesearch import search
import pyttsx3
import pywhatkit
import validators
import openai
import speedtest
import re
from PIL import Image
from io import BytesIO

# Define some helper functions first
def get_ip_address():
    ip = requests.get('https://api64.ipify.org').text
    return ip

def grammar_checker(text):
    url = "https://api.textgears.com/check.php"
    params = {
        "text": text,
        "key": "your_api_key_here"
    }
    response = requests.get(url, params=params)
    data = response.json()
    if data["error"] == 0:
        return data["response"]["errors"]
    else:
        return "No grammar issues detected."

def speed_test():
    st = speedtest.Speedtest()
    download_speed = st.download() / 1_000_000  # Convert to Mbps
    upload_speed = st.upload() / 1_000_000  # Convert to Mbps
    ping = st.results.ping
    return download_speed, upload_speed, ping

def reverse_image_search(image_path):
    # Using an external API for reverse image search like Google Custom Search API
    # Assuming the image is uploaded and URL is available
    image_url = "http://example.com/path/to/your/image.jpg"  # Replace with the actual URL
    search_results = search(image_url, num_results=5)
    return search_results

def paraphrase_text(text):
    openai.api_key = 'your_openai_api_key'
    prompt = f"Paraphrase this text: {text}"
    response = openai.Completion.create(engine="text-davinci-003", prompt=prompt, max_tokens=150)
    return response.choices[0].text.strip()

def plagiarism_checker(text):
    # This would typically require third-party APIs like Copyscape or similar
    # Since this is just a placeholder, you can use an external service or API
    return "Plagiarism checker is unavailable for local use. Use an API."

def ai_detector(text):
    # Placeholder for AI content detection; needs third-party service
    return "AI Detector is unavailable locally."

def pdf_to_word(pdf_path):
    from pdf2docx import Converter
    cv = Converter(pdf_path)
    output_path = pdf_path.replace('.pdf', '.docx')
    cv.convert(output_path)
    cv.close()
    return output_path

def seo_score_checker(website_url):
    url = f"https://api.seositecheckup.com/v1/score/{website_url}"
    # Placeholder for a real API request to check SEO score
    return "SEO Score API result not available for demo."

def emojis():
    return ["😀", "😊", "😍", "😎", "😂", "🤔", "😢", "🤩"]

def citation_generator(text):
    # Placeholder for generating citations, can use some Citation API or library
    return f"Citation generated for: {text[:30]}..."

def logo_maker():
    # Placeholder function for logo maker, ideally connects to a logo making API
    return "Logo Maker is not available in this demo."

# Main function that lets user choose which tool to use
def main():
    print("Welcome to the Multi-Tool Assistant")
    print("Choose a tool:")
    print("1. Plagiarism Checker")
    print("2. Paraphrasing Tool")
    print("3. AI Detector")
    print("4. Free Grammar Checker")
    print("5. Reverse Image Search")
    print("6. Logo Maker")
    print("7. What is My IP")
    print("8. PDF To Word")
    print("9. Internet Speed Test")
    print("10. Website SEO Score Checker")
    print("11. Emojis")
    print("12. Citation Generator")
    print("13. AI Humanizer")

    choice = input("Enter the number of the tool you want to use: ")

    if choice == "1":
        text = input("Enter the text to check for plagiarism: ")
        print(plagiarism_checker(text))
    
    elif choice == "2":
        text = input("Enter the text to paraphrase: ")
        print(paraphrase_text(text))
    
    elif choice == "3":
        text = input("Enter the text to detect AI content: ")
        print(ai_detector(text))
    
    elif choice == "4":
        text = input("Enter the text to check grammar: ")
        print(grammar_checker(text))
    
    elif choice == "5":
        image_path = input("Enter image file path for reverse image search: ")
        print(reverse_image_search(image_path))
    
    elif choice == "6":
        print(logo_maker())
    
    elif choice == "7":
        print("Your IP address is:", get_ip_address())
    
    elif choice == "8":
        pdf_path = input("Enter PDF file path: ")
        print(pdf_to_word(pdf_path))
    
    elif choice == "9":
        download, upload, ping = speed_test()
        print(f"Download speed: {download:.2f} Mbps\nUpload speed: {upload:.2f} Mbps\nPing: {ping} ms")
    
    elif choice == "10":
        website_url = input("Enter website URL for SEO score: ")
        print(seo_score_checker(website_url))
    
    elif choice == "11":
        print("Here are some emojis:", emojis())
    
    elif choice == "12":
        text = input("Enter text to generate a citation for: ")
        print(citation_generator(text))
    
    elif choice == "13":
        print("AI Humanizer tool not available in demo.")
    
    else:
        print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()

How it works:

    Plagiarism Checker: Placeholder for plagiarism checking; requires a third-party API like Copyscape or others.
    Paraphrasing Tool: Uses OpenAI's GPT-3 or GPT-4 API to paraphrase text.
    AI Detector: Placeholder for detecting AI-generated content; you would need a service like OpenAI's "AI Text Classifier."
    Free Grammar Checker: Uses the TextGears API to check grammar.
    Reverse Image Search: Placeholder for image search functionality (Google Custom Search API).
    Logo Maker: A placeholder for logo creation, ideally connected to a logo design API.
    What is My IP: Uses the ipify API to fetch the public IP.
    PDF to Word: Uses the pdf2docx Python library to convert PDFs to Word documents.
    Internet Speed Test: Uses the speedtest-cli package to measure download/upload speeds and ping.
    Website SEO Score Checker: Placeholder for a website SEO analysis tool.
    Emojis: Returns a list of sample emojis.
    Citation Generator: Placeholder for generating citations for a given text (could use a citation API or tool).
    AI Humanizer: Placeholder for AI humanization functionality (specific tool/API not included here).

Notes:

    API Keys: You need to substitute placeholders like your_api_key_here with actual API keys from services like TextGears, OpenAI, etc.

    Dependencies: Some tools require external libraries (e.g., requests, pyttsx3, speedtest-cli, pdf2docx, openai), which need to be installed. You can install them using pip, e.g.:

    pip install requests pyttsx3 pywhatkit speedtest-cli pdf2docx openai

    Error Handling: You should add proper error handling for APIs that may fail, or for incorrect inputs.

    Extend Functionality: This script is just a template. You can extend it with more advanced functionalities, such as real-time AI content detection, more sophisticated SEO analysis, or better reverse image search.

This script acts as a starting point to build the integrated tools you are asking for, but depending on your requirements, you may need to adjust the functionality or integrate with more APIs and external services.
