# web-scrapping-on-gov-webpage
done this web scrapping using selenium for an internshala assignment for internship 
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import Select
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

def fetch_survey_numbers(district, mandal, village):
    # Initialize Chrome webdriver
    driver = webdriver.Chrome()

    # Navigate to the website
    driver.get("https://dharani.telangana.gov.in/knowLandStatus")

    # Select District
    district_dropdown = Select(driver.find_element(By.ID, "district"))
    district_dropdown.select_by_visible_text(district)

    # Select Mandal
    mandal_dropdown = Select(driver.find_element(By.ID, "mandal"))
    mandal_dropdown.select_by_visible_text(mandal)

    # Select Village
    village_dropdown = Select(driver.find_element(By.ID, "village"))
    village_dropdown.select_by_visible_text(village)

    # Click on Submit button to fetch Survey numbers
    driver.find_element(By.ID, "button").click()

    # Wait for Survey numbers to load
    WebDriverWait(driver, 10).until(EC.presence_of_element_located((By.ID, "survey_no")))

    # Extract Survey numbers
    survey_numbers_element = driver.find_element(By.ID, "survey_no")
    survey_numbers = survey_numbers_element.text.split("\n")

    # Close the browser
    driver.quit()

    return survey_numbers

# Example usage
district = "YourDistrict"
mandal = "YourMandal"
village = "YourVillage"

survey_numbers = fetch_survey_numbers(district, mandal, village)
print("Survey numbers:", survey_numbers)
