# Xpath-task
This task covers different types of XPath locators used in Selenium WebDriver with Python to identify and interact with web elements such as input fields, buttons, labels, and headings.
# Program

```
python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait, Select
from selenium.webdriver.support import expected_conditions as EC
from selenium.common.exceptions import WebDriverException, TimeoutException


# Browser setup
driver = webdriver.Chrome()
driver.maximize_window()
wait = WebDriverWait(driver, 10)

url = "https://www.selenium.dev/selenium/web/web-form.html"


def find_element(xpath):
    return wait.until(
        EC.presence_of_element_located((By.XPATH, xpath))
    )


def click_element(xpath):
    element = wait.until(
        EC.element_to_be_clickable((By.XPATH, xpath))
    )
    element.click()
    return element


try:
    # TC01 - Open student registration page using get()
    driver.get(url)
    find_element("//input[@name='my-text']")
    print("TC01 Passed: Registration page opened")

    # TC02 - Locate username using an attribute
    username = find_element("//input[@name='my-text']")
    username.clear()
    username.send_keys("AJ")
    print("TC02 Passed: Username entered")

    # TC03 - Enter password using an attribute
    password = find_element("//input[@name='my-password']")
    password.send_keys("pass1234")
    print("TC03 Passed: Password entered")

    # TC04 - Locate Submit button using text()
    submit_button = find_element("//button[text()='Submit']")
    print("TC04 Passed: Submit button:", submit_button.text)

    # TC05 - Locate textarea using contains()
    textarea = find_element("//textarea[contains(@name,'textarea')]")
    textarea.send_keys("This is Selenium XPath testing")
    print("TC05 Passed: Textarea entered")

    # TC06 - Locate input using starts-with()
    datalist = find_element("//input[starts-with(@name,'my-data')]")
    datalist.send_keys("One")
    print("TC06 Passed: Datalist input entered")

    # TC07 - Locate input using two attributes and
    password = find_element(
        "//input[@name='my-password' and @type='password']"
    )
    print("TC07 Passed: Password field found using AND")

    # TC08 - Locate input using or
    text_or_password = find_element(
        "//input[@name='my-text' or @name='my-password']"
    )
    print("TC08 Passed: Element found using OR")

    # TC09 - Find parent element using parent::
    parent = find_element("//input[@name='my-text']/parent::*")
    print("TC09 Passed: Parent tag:", parent.tag_name)

    # TC10 - Find form using ancestor::
    form = find_element("//input[@name='my-text']/ancestor::form")
    print("TC10 Passed: Form found:", form.tag_name)

    # TC11 - Find input descendants of the form
    child_inputs = driver.find_elements(
        By.XPATH, "//form/descendant::input"
    )
    print("TC11 Passed: Input fields inside form:", len(child_inputs))

    # TC12 - Find next input using following::
    following_element = find_element(
        "//input[@name='my-text']/following::input[1]"
    )
    print(
        "TC12 Passed: Following input:",
        following_element.get_attribute("name")
    )

    # TC13 - Select checkbox
    checkbox = find_element("//input[@name='my-check']")
    if not checkbox.is_selected():
        checkbox.click()
    print("TC13 Passed: Checkbox selected")

    # TC14 - Select radio button
    radio = find_element("//input[@name='my-radio']")
    if not radio.is_selected():
        radio.click()
    print("TC14 Passed: Radio button selected")

    # TC15 - Select dropdown option
    dropdown = Select(find_element("//select[@name='my-select']"))
    dropdown.select_by_visible_text("Two")
    print("TC15 Passed: Dropdown option Two selected")

    # TC16 - Locate second input using XPath index
    second_textbox = find_element("(//input)[2]")
    print(
        "TC16 Passed: Second input:",
        second_textbox.get_attribute("name")
    )

    # TC17 - Submit the form and verify response
    click_element("//button[text()='Submit']")

    success_message = wait.until(
        EC.visibility_of_element_located(
            (By.XPATH, "//*[contains(text(),'Received')]")
        )
    )
    print("TC17 Passed: Submitted message:", success_message.text)

    # TC18 - Return to the form and find all input elements
    driver.get(url)
    find_element("//input[@name='my-text']")

    all_inputs = driver.find_elements(By.XPATH, "//input")
    print("TC18 Passed: Total input fields:", len(all_inputs))

    # TC19 - Locate dynamic input using contains()
    dynamic_element = find_element(
        "//input[contains(@name,'my-')]"
    )
    print(
        "TC19 Passed: Dynamic element:",
        dynamic_element.get_attribute("name")
    )

    # TC20 - Complete form automation using multiple XPath concepts
    username = find_element("//input[@name='my-text']")
    username.clear()
    username.send_keys("DK")

    password = find_element("//input[@name='my-password']")
    password.clear()
    password.send_keys("pass1234")

    textarea = find_element(
        "//textarea[contains(@name,'textarea')]"
    )
    textarea.clear()
    textarea.send_keys("Complete XPath Automation Test")

    dropdown = Select(find_element("//select[@name='my-select']"))
    dropdown.select_by_visible_text("Three")

    checkbox = find_element("//input[@name='my-check']")
    if not checkbox.is_selected():
        checkbox.click()

    radio = find_element("//input[@name='my-radio']")
    if not radio.is_selected():
        radio.click()

    click_element("//button[text()='Submit']")

    success_message = wait.until(
        EC.visibility_of_element_located(
            (By.XPATH, "//*[contains(text(),'Received')]")
        )
    )

    print("TC20 Passed: Complete XPath automation finished")
    print("Final response:", success_message.text)

except TimeoutException:
    print("Test failed: Expected element was not found in time.")
    print("Check the page, XPath locator, and internet connection.")

except WebDriverException as e:
    print("Browser or website error:", e)
    print("Check your internet, DNS, and ChromeDriver setup.")

finally:
    input("Press Enter to close browser...")
    driver.quit()
```

# output:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/72d7bb3e-40b8-4705-9627-1d0e9b43337e" />

