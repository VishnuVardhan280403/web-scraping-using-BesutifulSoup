import requests
from bs4 import BeautifulSoup
import pandas as pd

# URL for Adobe-related jobs in the US on LinkedIn
url = "https://www.linkedin.com/jobs/search?keywords=Adobe_experience_manager&location=United%20States"

headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36'
}

# Fetch the HTML content
html_page = requests.get(url, headers=headers)

# Parse the HTML with BeautifulSoup
soup = BeautifulSoup(html_page.content, 'html.parser')

# Initialize lists to hold job information
job_titles = []
company_names = []
locations = []

# Find all job listings
for job_card in soup.find_all('div', class_='base-card'):
    title_element = job_card.find('h3', class_='base-search-card__title')
    company_element = job_card.find('h4', class_='base-search-card__subtitle')
    location_element = job_card.find('span', class_='job-search-card__location')

    # Check if the job is posted by Adobe
    if company_element and "Adobe" in company_element.text.strip():
        job_titles.append(title_element.text.strip())
        print(f"Title: {title_element.text.strip()}")

        company_names.append(company_element.text.strip())
        print(f"Company: {company_element.text.strip()}")

        if location_element:
            locations.append(location_element.text.strip())
            print(f"Location: {location_element.text.strip()}")
        else:
            locations.append(None)  # Handle missing locations

# Create a Pandas DataFrame
df = pd.DataFrame({
    'Job Title': job_titles,
    'Company': company_names,
    'Location': locations
})

# Export the DataFrame to an Excel file
df.to_excel("adobe_jobs_us.xlsx", index=False)
print("Data exported to adobe_jobs_us.xlsx")

# Optional: Download the file in a Jupyter Notebook or Google Colab environment
#from google.colab import files
#files.download('adobe_jobs_us.xlsx')
