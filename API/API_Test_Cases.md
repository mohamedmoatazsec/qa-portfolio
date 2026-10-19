# API test cases - DummyJSON

Mohamed Moataz | Software testing portfolio | 19 October 2026

Recorded result: **10 requests passed; 55 assertions passed.** The Postman collection was executed with Newman 6.2.3 against https://dummyjson.com over HTTPS. All requests are read-only.

Test basis: [product documentation](https://dummyjson.com/docs/products), [authentication documentation](https://dummyjson.com/docs/auth), and the fixture assumptions stated below. DummyJSON is a separate exercise from SauceDemo.

## Detailed cases


### API-01 — Retrieve one existing product

- **Type:** Positive / functional.
- **Preconditions:** Public product fixture with ID 1 exists; no login required.
- **Input:** GET https://dummyjson.com/products/1; Accept: application/json; no authentication or request body.
- **Steps:** Open this request in Postman, send it, inspect status and JSON body, and review each Tests result; alternatively run the full collection.
- **Expected:** HTTP 200; JSON object with id 1, a non-empty title, a non-negative numeric price, and a category.
- **Actual:** HTTP 200. Product ID 1; title "Essence Mascara Lash Princess"; price 9.99; category beauty.
- **Result:** PASS; 6/6 assertions passed; response time 237 ms.
- **Evidence:** ../Evidence/API/Live_API_Execution_Evidence.json, cases[0]; request sent 2026-10-19T10:24:28.255Z, response received 2026-10-19T10:24:28.493Z.
- **Source:** https://dummyjson.com/docs/products

### API-02 — Limit the first page and select fields

- **Type:** Positive / pagination and projection.
- **Preconditions:** At least three product fixtures exist; public endpoint available.
- **Input:** GET https://dummyjson.com/products?limit=3&skip=0&select=title,price; Accept: application/json; no authentication or request body.
- **Steps:** Open this request in Postman, send it, inspect status and JSON body, and review each Tests result; alternatively run the full collection.
- **Expected:** HTTP 200; three products, skip 0, limit 3; each product has only id, title and price.
- **Actual:** HTTP 200. 3 products; skip 0; limit 3; IDs 1, 2, 3; returned keys id, title, price.
- **Result:** PASS; 6/6 assertions passed; response time 108 ms.
- **Evidence:** ../Evidence/API/Live_API_Execution_Evidence.json, cases[1]; request sent 2026-10-19T10:24:28.803Z, response received 2026-10-19T10:24:28.913Z.
- **Source:** https://dummyjson.com/docs/products

### API-03 — Skip the first three product fixtures

- **Type:** Positive / pagination.
- **Preconditions:** Default product fixture order begins with IDs 1, 2, 3; at least six fixtures exist. This fixture-order assumption was checked during exploration.
- **Input:** GET https://dummyjson.com/products?limit=3&skip=3&select=title,price; Accept: application/json; no authentication or request body.
- **Steps:** Open this request in Postman, send it, inspect status and JSON body, and review each Tests result; alternatively run the full collection.
- **Expected:** HTTP 200; three products, skip 3, limit 3; IDs 1, 2, 3 are excluded; no duplicate IDs.
- **Actual:** HTTP 200. 3 products; skip 3; limit 3; returned IDs 4, 5, 6.
- **Result:** PASS; 6/6 assertions passed; response time 102 ms.
- **Evidence:** ../Evidence/API/Live_API_Execution_Evidence.json, cases[2]; request sent 2026-10-19T10:24:29.190Z, response received 2026-10-19T10:24:29.293Z.
- **Source:** https://dummyjson.com/docs/products

### API-04 — Search for a known product keyword

- **Type:** Positive / search.
- **Preconditions:** At least one fixture has mascara in its title, description, or tags; verified during exploration.
- **Input:** GET https://dummyjson.com/products/search?q=mascara; Accept: application/json; no authentication or request body.
- **Steps:** Open this request in Postman, send it, inspect status and JSON body, and review each Tests result; alternatively run the full collection.
- **Expected:** HTTP 200; non-empty results; returned product text matches mascara and IDs are unique.
- **Actual:** HTTP 200. 1 result(s), total 1; titles: Essence Mascara Lash Princess.
- **Result:** PASS; 6/6 assertions passed; response time 95 ms.
- **Evidence:** ../Evidence/API/Live_API_Execution_Evidence.json, cases[3]; request sent 2026-10-19T10:24:29.602Z, response received 2026-10-19T10:24:29.698Z.
- **Source:** https://dummyjson.com/docs/products

### API-05 — Search with a keyword that has no matches

- **Type:** Negative / empty-result equivalence class.
- **Preconditions:** The unique keyword qa_no_match_8e521d7a is absent from the public fixtures.
- **Input:** GET https://dummyjson.com/products/search?q=qa_no_match_8e521d7a; Accept: application/json; no authentication or request body.
- **Steps:** Open this request in Postman, send it, inspect status and JSON body, and review each Tests result; alternatively run the full collection.
- **Expected:** HTTP 200; products is an empty array; total is 0 and skip is 0. A valid search with no results is not a missing endpoint.
- **Actual:** HTTP 200. products []; total 0; skip 0; limit 0.
- **Result:** PASS; 5/5 assertions passed; response time 97 ms.
- **Evidence:** ../Evidence/API/Live_API_Execution_Evidence.json, cases[4]; request sent 2026-10-19T10:24:30.000Z, response received 2026-10-19T10:24:30.097Z.
- **Source:** https://dummyjson.com/docs/products

### API-06 — Filter products by category

- **Type:** Positive / category filter.
- **Preconditions:** The documented category beauty exists and has products.
- **Input:** GET https://dummyjson.com/products/category/beauty; Accept: application/json; no authentication or request body.
- **Steps:** Open this request in Postman, send it, inspect status and JSON body, and review each Tests result; alternatively run the full collection.
- **Expected:** HTTP 200; non-empty products array; every returned product belongs to beauty; IDs are unique.
- **Actual:** HTTP 200. 5 products; all categories beauty; total 5.
- **Result:** PASS; 6/6 assertions passed; response time 263 ms.
- **Evidence:** ../Evidence/API/Live_API_Execution_Evidence.json, cases[5]; request sent 2026-10-19T10:24:30.403Z, response received 2026-10-19T10:24:30.667Z.
- **Source:** https://dummyjson.com/docs/products

### API-07 — Sort products by ascending price

- **Type:** Positive / sorting.
- **Preconditions:** At least five product fixtures with numeric prices exist.
- **Input:** GET https://dummyjson.com/products?sortBy=price&order=asc&limit=5&select=title,price; Accept: application/json; no authentication or request body.
- **Steps:** Open this request in Postman, send it, inspect status and JSON body, and review each Tests result; alternatively run the full collection.
- **Expected:** HTTP 200; five products; numeric prices in non-decreasing order, including equal prices as valid.
- **Actual:** HTTP 200. Prices in returned order: 0.79, 0.99, 0.99, 1.29, 1.49; limit 5.
- **Result:** PASS; 6/6 assertions passed; response time 386 ms.
- **Evidence:** ../Evidence/API/Live_API_Execution_Evidence.json, cases[6]; request sent 2026-10-19T10:24:30.955Z, response received 2026-10-19T10:24:31.341Z.
- **Source:** https://dummyjson.com/docs/products

### API-08 — Retrieve category names for filter controls

- **Type:** Positive / response schema.
- **Preconditions:** Public product category list is available.
- **Input:** GET https://dummyjson.com/products/category-list; Accept: application/json; no authentication or request body.
- **Steps:** Open this request in Postman, send it, inspect status and JSON body, and review each Tests result; alternatively run the full collection.
- **Expected:** HTTP 200; non-empty array of unique non-empty strings; documented example category beauty is included.
- **Actual:** HTTP 200. 24 unique category names; beauty is present.
- **Result:** PASS; 6/6 assertions passed; response time 408 ms.
- **Evidence:** ../Evidence/API/Live_API_Execution_Evidence.json, cases[7]; request sent 2026-10-19T10:24:31.588Z, response received 2026-10-19T10:24:31.997Z.
- **Source:** https://dummyjson.com/docs/products

### API-09 — Reject a non-existent product identifier

- **Type:** Negative / resource not found.
- **Preconditions:** Product ID 999999 does not exist. HTTP 404 and a safe JSON error are exploratory acceptance expectations, rather than an explicit guarantee in the product prose documentation.
- **Input:** GET https://dummyjson.com/products/999999; Accept: application/json; no authentication or request body.
- **Steps:** Open this request in Postman, send it, inspect status and JSON body, and review each Tests result; alternatively run the full collection.
- **Expected:** HTTP 404; JSON object with a non-empty message; no product id, title, or price fields.
- **Actual:** HTTP 404. Error message: Product with id '999999' not found.
- **Result:** PASS; 4/4 assertions passed; response time 379 ms.
- **Evidence:** ../Evidence/API/Live_API_Execution_Evidence.json, cases[8]; request sent 2026-10-19T10:24:32.287Z, response received 2026-10-19T10:24:32.667Z.
- **Source:** https://dummyjson.com/docs/products

### API-10 — Reject access to current user without a token

- **Type:** Negative / authentication.
- **Preconditions:** No Authorization header, no access-token cookie, no login; collection uses No Auth. HTTP 401 is the expected authentication convention; docs show that a token is needed.
- **Input:** GET https://dummyjson.com/auth/me; Accept: application/json; no authentication or request body.
- **Steps:** Open this request in Postman, send it, inspect status and JSON body, and review each Tests result; alternatively run the full collection.
- **Expected:** HTTP 401; JSON error with a non-empty message; no user identity or access token in the body.
- **Actual:** HTTP 401. Error message: Access Token is required.
- **Result:** PASS; 4/4 assertions passed; response time 419 ms.
- **Evidence:** ../Evidence/API/Live_API_Execution_Evidence.json, cases[9]; request sent 2026-10-19T10:24:32.941Z, response received 2026-10-19T10:24:33.360Z.
- **Source:** https://dummyjson.com/docs/auth

## Run the collection

1. Import `Live_DummyJSON.postman_collection.json` into Postman.
2. Keep `baseUrl` set to `https://dummyjson.com` and use No Auth.
3. Clear existing authentication cookies for this host before API-10.
4. Run all ten requests once and review the response bodies and assertions.

The recorded execution and original response bodies are in [the API evidence](../Evidence/API/Live_API_Execution_Evidence.json). The collection hash in that record matches the included JSON file.
