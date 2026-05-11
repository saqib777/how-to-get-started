# pytest Quickstart — From Zero to Running Tests

The fastest path to writing and running your first Python tests.

---

## Install

```bash
pip install pytest pytest-html
```

---

## Your First Test

Create a file `test_calculator.py`:

```python
def add(a, b):
    return a + b

def test_add_positive():
    assert add(2, 3) == 5

def test_add_negative():
    assert add(-1, 1) == 0

def test_add_zero():
    assert add(0, 0) == 0
```

Run it:

```bash
pytest test_calculator.py -v
```

---

## Test Discovery Rules

pytest automatically finds tests that follow these rules:

- Files named `test_*.py` or `*_test.py`
- Functions named `test_*`
- Classes named `Test*`
- Methods named `test_*` inside those classes

---

## Assertions

pytest gives detailed failure messages for any assertion:

```python
assert result == expected
assert result != wrong_value
assert result is None
assert result is not None
assert value in collection
assert value > threshold
assert isinstance(obj, MyClass)
```

---

## Fixtures

Fixtures provide reusable setup for tests:

```python
import pytest

@pytest.fixture
def sample_list():
    return [1, 2, 3, 4, 5]

def test_length(sample_list):
    assert len(sample_list) == 5

def test_sum(sample_list):
    assert sum(sample_list) == 15
```

### Fixture scopes

```python
@pytest.fixture(scope="function")  # default — new instance per test
@pytest.fixture(scope="class")     # shared within a test class
@pytest.fixture(scope="module")    # shared within a file
@pytest.fixture(scope="session")   # shared for entire test run
```

---

## Parametrize — Run One Test with Many Inputs

```python
import pytest

@pytest.mark.parametrize("a, b, expected", [
    (1, 2, 3),
    (0, 0, 0),
    (-1, 1, 0),
    (100, 200, 300),
])
def test_add(a, b, expected):
    assert add(a, b) == expected
```

---

## Markers

Mark tests to run subsets:

```python
@pytest.mark.slow
def test_heavy_operation():
    ...

@pytest.mark.skip(reason="not implemented yet")
def test_future_feature():
    ...

@pytest.mark.xfail(reason="known bug #123")
def test_known_broken():
    ...
```

Run only slow tests:
```bash
pytest -m slow
```

---

## Useful CLI Flags

```bash
pytest -v                    # verbose output
pytest -s                    # show print statements
pytest --tb=short            # shorter tracebacks
pytest -x                    # stop on first failure
pytest -k "login"            # run tests matching "login"
pytest --durations=10        # show 10 slowest tests
pytest --html=report.html    # generate HTML report
pytest --cov=src             # coverage report
```

---

## conftest.py

Shared fixtures go in `conftest.py` — automatically loaded by pytest:

```python
# conftest.py
import pytest

@pytest.fixture(scope="session")
def base_url():
    return "https://example.com"
```

Every test file in the same directory can use `base_url` without importing.
