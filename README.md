# Senior QA - API E2E Automation

Postman end-to-end API tests for the [Simple Grocery Store API](https://simple-grocery-store-api.click).

## Project structure

- `collections/` - Postman collection containing the API test requests.
- `environments/` - Postman environment with the API base URL and variables.
- `reports/` - Destination for generated test reports; report files are not committed by default.

## Run the tests

Install [Node.js](https://nodejs.org/) and Newman:

```bash
npm install --global newman
```

Run the collection from the project root:

```bash
newman run "collections/Senior QA - API E2E Automation.postman_collection.json" \
  --environment "environments/Senior QA - Simple Grocery Store.postman_environment.json"
```

The requests run in sequence: register an API client, create a cart, add an item, create an order, and retrieve the order. The registration request saves the access token to the environment for later requests.

## CI

The GitHub Actions workflow in `.github/workflows/api-tests.yml` runs the complete collection on pushes and pull requests. It uploads the HTML test report as the `postman-api-test-report` artifact, including when the API tests fail.

## Environment and secrets

The checked-in environment contains the API base URL and blank runtime variables. Keep credentials and local environment overrides out of version control; `.gitignore` excludes `secrets/` and `*.local.json`.
