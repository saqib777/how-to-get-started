# Postman Basics for API Testing

The fastest way to explore and test APIs without writing code.

---

## Install

Download from postman.com/downloads — free for individual use.

---

## Making Your First Request

1. Click **New** → **HTTP Request**
2. Select method (GET, POST, etc.)
3. Enter URL: `https://jsonplaceholder.typicode.com/posts/1`
4. Click **Send**
5. See the response in the bottom panel

---

## Request Types

| Method | When to use |
|--------|-------------|
| GET | Retrieve data |
| POST | Create new resource |
| PUT | Replace entire resource |
| PATCH | Update part of resource |
| DELETE | Remove resource |

---

## Sending a POST Request

1. Select **POST**
2. Enter URL
3. Click **Body** tab → select **raw** → select **JSON**
4. Enter body:

```json
{
    "title": "Test Post",
    "body": "This is content",
    "userId": 1
}
```

5. Click **Send** → should get 201 Created

---

## Headers

Click **Headers** tab to add:

| Key | Value |
|-----|-------|
| Content-Type | application/json |
| Authorization | Bearer your_token_here |
| Accept | application/json |

---

## Collections — Organise Requests

1. Click **Collections** in sidebar → **New Collection**
2. Name it (e.g. "ReqRes API Tests")
3. Add requests to the collection
4. Run entire collection with **Collection Runner**

---

## Environments — Manage Variables

Instead of hardcoding URLs and tokens, use variables:

1. Click **Environments** → **New Environment**
2. Add variables:
   - `base_url` = `https://reqres.in/api`
   - `token` = `your_token`
3. Use in requests: `{{base_url}}/users`

Switch between Dev/Staging/Prod by changing environment.

---

## Tests Tab — Automated Assertions

Write JavaScript assertions in the **Tests** tab:

```javascript
// Status code
pm.test("Status is 200", () => {
    pm.response.to.have.status(200);
});

// Response has field
pm.test("Has user id", () => {
    const data = pm.response.json();
    pm.expect(data.id).to.exist;
});

// Response time
pm.test("Response under 2s", () => {
    pm.expect(pm.response.responseTime).to.be.below(2000);
});

// Content type
pm.test("Content-Type is JSON", () => {
    pm.expect(pm.response.headers.get("Content-Type")).to.include("application/json");
});
```

---

## Pre-request Scripts

Run code before the request — useful for dynamic tokens:

```javascript
// Set timestamp variable
pm.environment.set("timestamp", new Date().toISOString());

// Generate random email
pm.environment.set("email", `test_${Math.random().toString(36).slice(2)}@test.com`);
```

---

## Export and Share

1. Right-click collection → **Export**
2. Save as JSON
3. Commit to your repo under `postman/` folder
4. Team imports with **Import** → select file
