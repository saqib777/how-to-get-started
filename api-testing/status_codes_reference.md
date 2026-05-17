# HTTP Status Codes - Complete Reference for Testers

Every status code you will encounter in API testing.

---

## 2xx - Success

| Code | Name | When You See It |
|------|------|-----------------|
| 200 | OK | Successful GET, PUT, PATCH |
| 201 | Created | Successful POST (resource created) |
| 202 | Accepted | Request received, processing async |
| 204 | No Content | Successful DELETE (no body) |

**Test assertions for 2xx:**
```python
assert response.status_code == 200
assert response.status_code in [200, 201]
assert response.json()["id"] is not None
```

---

## 3xx - Redirection

| Code | Name | When You See It |
|------|------|-----------------|
| 301 | Moved Permanently | URL has permanently changed |
| 302 | Found | Temporary redirect |
| 304 | Not Modified | Cached version is still valid |

---

## 4xx — Client Errors (Your Fault)

| Code | Name | Common Cause |
|------|------|-------------|
| 400 | Bad Request | Invalid JSON, missing required field |
| 401 | Unauthorized | No token or token missing |
| 403 | Forbidden | Token valid but no permission |
| 404 | Not Found | Resource does not exist |
| 405 | Method Not Allowed | POST on a GET-only endpoint |
| 409 | Conflict | Duplicate resource (email already exists) |
| 422 | Unprocessable Entity | Validation error (invalid email format) |
| 429 | Too Many Requests | Rate limit exceeded |

**Test assertions for 4xx:**
```python
def test_missing_auth():
    r = requests.get(url)   # no auth header
    assert r.status_code == 401

def test_not_found():
    r = requests.get(f"{url}/99999")
    assert r.status_code == 404
    assert "error" in r.json() or r.json() == {}

def test_duplicate():
    requests.post(url, json=payload)   # first create
    r = requests.post(url, json=payload)   # duplicate
    assert r.status_code == 409
```

---

## 5xx — Server Errors (Their Fault)

| Code | Name | When You See It |
|------|------|-----------------|
| 500 | Internal Server Error | Unhandled exception on server |
| 502 | Bad Gateway | Upstream server failed |
| 503 | Service Unavailable | Server down or overloaded |
| 504 | Gateway Timeout | Upstream timed out |

**5xx means the server is broken — escalate, do not retry indefinitely.**

---

## Testing All Codes Systematically

```python
import pytest
import requests

BASE = "https://reqres.in/api"

@pytest.mark.parametrize("user_id, expected", [
    (1,    200),   # exists
    (999,  404),   # not found
])
def test_user_status_codes(user_id, expected):
    r = requests.get(f"{BASE}/users/{user_id}")
    assert r.status_code == expected


@pytest.mark.parametrize("payload, expected", [
    ({"email": "eve.holt@reqres.in", "password": "pistol"}, 200),
    ({"email": "peter@klaven"},                              400),
])
def test_register_status_codes(payload, expected):
    r = requests.post(f"{BASE}/register", json=payload)
    assert r.status_code == expected
```
