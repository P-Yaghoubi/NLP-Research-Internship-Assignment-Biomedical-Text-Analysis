# NLP-Research-Internship-Assignment-Biomedical-Text-Analysis


import requests
from bs4 import BeautifulSoup

url = "https://pubmed.ncbi.nlm.nih.gov/?term=immunology+cancer"

response = requests.get(url)
html = response.content

soup = BeautifulSoup(html, "html.parser")


articles = soup.find_all("a", class_="Cancer Immonology")

for article in articles:
    article_url = "https://pubmed.ncbi.nlm.nih.gov" + article["href"]
    article_response = requests.get(article_url)
    article_html = article_response.content
    article_soup = BeautifulSoup(article_html, "html.parser")
    
    abstract = article_soup.find("div", class_="abstract-content").text.strip()
    
    print("article", articles.text)
    print("abstract", abstract)
    print("="*50)
