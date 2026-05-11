# API Testing with Python requests

A practical guide to testing REST APIs using the requests library.

---

## Install

```bash
pip install requests pytest
```

---

## Basic Requests

```python
import requests

# GET
response = requests.get("https://jsonplaceholder.typicode.com/posts/1")

# POST
response = requests.post(
    "https://jsonplaceholder.typicode.com/posts",
    json={"title": "Test", "body": "Content", "userId": 1}
)

# PUT
response = requests.put(
    "https://jsonplaceholder.typicode.com/posts/1",
    json={"id": 1, "title": "Updated"}
)

# PATCH
response = requests.patch(
    "https://jsonplaceholder.typicode.com/posts/1",
    json={"title": "Patched Title"}
)

# DELETE
response = requests.delete("https://jsonplaceholder.typicode.com/posts/1")
```

---

## Reading Responses

```python
response.status_code       # 200, 201, 404...
response.json()            # parse JSON body
response.text              # raw string body
response.headers           # dict of response headers
response.elapsed           # timedelta of request duration
response.url               # final URL after redirects
```

---

## Common Assertions in Tests

```python
import pytest
import requests

BASE_URL = "https://jsonplaceholder.typicode.com"

def test_get_post():
    r = requests.get(f"{BASE_URL}/posts/1")
    assert r.status_code == 200
    data = r.json()
    assert data["id"] == 1
    assert "title" in data
    assert "body" in data

def test_create_post():
    payload = {"title": "New Post", "body": "Content", "userId": 1}
    r = requests.post(f"{BASE_URL}/posts", json=payload)
    assert r.status_code == 201
    assert r.json()["title"] == "New Post"

def test_not_found():
    r = requests.get(f"{BASE_URL}/posts/99999")
    assert r.status_code == 404

def test_response_time():
    r = requests.get(f"{BASE_URL}/posts/1")
    assert r.elapsed.total_seconds() < 3.0

def test_content_type():
    r = requests.get(f"{BASE_URL}/posts/1")
    assert "application/json" in r.headers["Content-Type"]
```

---

## Headers and Authentication

```python
# Custom headers
headers = {
    "Authorization": "Bearer your_token_here",
    "Content-Type": "application/json",
    "Accept": "application/json",
}
r = requests.get(url, headers=headers)

# Basic auth
r = requests.get(url, auth=("username", "password"))

# API key as query param
r = requests.get(url, params={"api_key": "your_key"})
```

---

## Sessions — Reuse Connections

```python
# Sessions persist cookies and headers across requests
session = requests.Session()
session.headers.update({"Authorization": "Bearer token"})

r1 = session.get(f"{BASE_URL}/users")
r2 = session.get(f"{BASE_URL}/posts")
# Both requests use the same auth header
```

---

## Status Code Reference

| Code | Meaning | When you see it |
|------|---------|-----------------|
| 200 | OK | Successful GET, PUT, PATCH |
| 201 | Created | Successful POST |
| 204 | No Content | Successful DELETE |
| 400 | Bad Request | Invalid input data |
| 401 | Unauthorized | Missing or invalid token |
| 403 | Forbidden | Token valid but no permission |
| 404 | Not Found | Resource does not exist |
| 409 | Conflict | Duplicate resource |
| 422 | Unprocessable | Validation error |
| 500 | Server Error | Bug on the server side |
