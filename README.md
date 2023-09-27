# NLP-Research-Internship-Assignment-Biomedical-Text-Analysis


import requests
from bs4 import BeautifulSoup
# URL related to searching for articles on cancer immunology
url = "https://pubmed.ncbi.nlm.nih.gov/?term=Cancer+Immunotherapy"
# Get the HTML page
response = requests.get(url)
html = response.content
# HTML processing using BeautifulSoup
soup = BeautifulSoup(html, "html.parser")
# Find all the titles of the articles on the page
articles = soup.find_all("a", class_="Cancer Immunotherapy")
# Display the abstract of each article
for article in articles:
    article_url = article['href']
    article_response = requests.get(article_url)
    article_html = article_response.content
    article_soup = BeautifulSoup(article_html, "html.parser")
    
    abstract = article_soup.find("div", class_="abstract-content").text.strip()
    
    print("article:", article.text)
    print("abstract:", abstract)
    print("="*50)


