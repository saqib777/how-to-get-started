# pytest Advanced Features

Beyond the basics — the features that make test suites professional.

---

## conftest.py — Shared Fixtures Across Files

```python
# conftest.py (place in root of tests/)
import pytest
import requests

@pytest.fixture(scope="session")
def api_client():
    session = requests.Session()
    session.headers.update({
        "Content-Type": "application/json",
        "Authorization": "Bearer test_token"
    })
    return session

@pytest.fixture(scope="function")
def clean_db():
    # Setup: seed test data
    yield
    # Teardown: clean up after test
```

Any test file in the same directory automatically has access to
`api_client` and `clean_db` without importing.

---

## Yield Fixtures — Setup and Teardown

```python
@pytest.fixture
def browser(driver):
    driver.get("https://example.com")
    yield driver          # test runs here
    driver.delete_all_cookies()
    driver.get("about:blank")
```

Everything before `yield` = setup.
Everything after `yield` = teardown (always runs, even if test fails).

---

## Parametrize with IDs

```python
@pytest.mark.parametrize("email, password, expected", [
    ("valid@test.com",   "Test@1234",  True),
    ("wrong@test.com",   "Test@1234",  False),
    ("valid@test.com",   "wrongpass",  False),
    ("",                 "Test@1234",  False),
], ids=["valid_login", "wrong_email", "wrong_password", "empty_email"])
def test_login(email, password, expected):
    result = attempt_login(email, password)
    assert result == expected
```

Named IDs make test output readable:
