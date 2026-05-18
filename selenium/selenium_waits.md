# Selenium Waits — The Complete Guide

Waits are the most common source of flaky tests.
This guide explains every type and when to use each.

---

## Why Waits Are Necessary

Modern web apps load content asynchronously.
An element may not exist in the DOM yet when your test looks for it.
Without waits, tests fail randomly — flaky tests lose trust.

---

## The Three Types

### 1. Implicit Wait — Set Once, Applied Everywhere

```python
driver.implicitly_wait(10)   # seconds
```

Tells Selenium to wait up to 10 seconds before throwing
`NoSuchElementException` for every `find_element` call.

**Pros:** Simple — one line covers everything.
**Cons:** Slows down tests when elements genuinely don't exist.
**Use:** As a safety net, set low (3-5 seconds).

---

### 2. Explicit Wait — Wait for a Specific Condition

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By

wait = WebDriverWait(driver, timeout=10)

# Wait until element is visible
element = wait.until(
    EC.visibility_of_element_located((By.ID, "result"))
)

# Wait until element is clickable
button = wait.until(
    EC.element_to_be_clickable((By.CSS_SELECTOR, ".submit-btn"))
)

# Wait until text appears in element
wait.until(
    EC.text_to_be_present_in_element((By.ID, "status"), "Success")
)

# Wait until URL contains string
wait.until(EC.url_contains("/dashboard"))

# Wait until element disappears
wait.until(EC.invisibility_of_element_located((By.ID, "loading-spinner")))

# Wait until title contains text
wait.until(EC.title_contains("Dashboard"))
```

**Pros:** Precise — waits for exactly what you need.
**Cons:** More verbose — one wait per action.
**Use:** Always prefer this over implicit wait for critical actions.

---

### 3. Fluent Wait — Custom Polling and Exceptions

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.common.exceptions import NoSuchElementException

wait = WebDriverWait(
    driver,
    timeout=20,
    poll_frequency=0.5,         # check every 500ms
    ignored_exceptions=[NoSuchElementException]
)

element = wait.until(
    EC.presence_of_element_located((By.ID, "dynamic-content"))
)
```

**Use:** Slow-loading elements, polling at custom intervals.

---

## All Expected Conditions

```python
EC.presence_of_element_located(locator)        # in DOM, not necessarily visible
EC.visibility_of_element_located(locator)      # visible and in DOM
EC.element_to_be_clickable(locator)            # visible and enabled
EC.text_to_be_present_in_element(locator, text)
EC.invisibility_of_element_located(locator)    # element gone or hidden
EC.url_contains(url_part)
EC.url_to_be(exact_url)
EC.title_contains(title_part)
EC.title_is(exact_title)
EC.alert_is_present()
EC.frame_to_be_available_and_switch_to_it(locator)
EC.number_of_windows_to_be(n)
EC.staleness_of(element)                       # element removed from DOM
```

---

## NEVER Use time.sleep()

```python
# BAD — wastes time even when element is ready in 0.5s
time.sleep(5)
driver.find_element(By.ID, "result").click()

# GOOD — waits only as long as needed
wait.until(EC.element_to_be_clickable((By.ID, "result"))).click()
```

`time.sleep()` creates slow, rigid, brittle tests.
Explicit waits create fast, flexible, reliable tests.

---

## Recommended Setup

```python
# conftest.py
@pytest.fixture
def driver():
    drv = webdriver.Chrome(...)
    drv.implicitly_wait(3)           # safety net
    drv.set_page_load_timeout(30)
    yield drv
    drv.quit()

# In page objects
self.wait = WebDriverWait(driver, timeout=10)  # explicit waits
```
