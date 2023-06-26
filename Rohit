import string
import threading
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import os

# Set the path to your ChromeDriver executable
chrome_driver_path = 'path_to_chromedriver.exe'

def perform_search(index, letter):
    # Create a ChromeDriver instance
    service = Service(chrome_driver_path)
    driver = webdriver.Chrome(service=service)

    # Open Google
    driver.get('https://www.google.com/')

    # Find the search input element and enter your search query
    search_input = driver.find_element(By.NAME, 'q')
    search_query = f'Search query for instance {index+1} {letter}'  # Append the alphabet to the search query
    search_input.send_keys(search_query)
    search_input.send_keys(Keys.RETURN)

    # Wait for the video result to appear and click on it
    video_xpath = "//div[@class='g']//h3[contains(text(),'YouTube')]/../following-sibling::div//a"
    video_result = WebDriverWait(driver, 10).until(EC.presence_of_element_located((By.XPATH, video_xpath)))
    video_result.click()

    # Close the browser
    driver.quit()

# Create threads for each alphabet
threads = []
for i, letter in enumerate(string.ascii_lowercase):
    thread = threading.Thread(target=perform_search, args=(i, letter))
    threads.append(thread)
    thread.start()

# Wait for all threads to finish
for thread in threads:
    thread.join()
