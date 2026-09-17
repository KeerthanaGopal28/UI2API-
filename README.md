# UI2API

UI2API is a React-based developer tool that compares a **UI/mock JSON structure with a live API response** to identify differences in the expected and actual data structure.

It automatically infers a schema from mock JSON, normalizes the inferred structure, recursively compares it with the API response, and presents missing fields, extra fields, and type mismatches in a structured diff view.

## Features

* Paste and edit mock JSON using a Monaco Editor
* Fetch JSON data directly from an API URL
* Automatically infer a schema from mock JSON
* Normalize inferred schema types and structures
* Recursively compare expected and actual API data
* Detect:

  * Missing fields
  * Extra fields
  * Type mismatches
  * Correctly matched fields
* Support nested objects and arrays
* Handle required and optional fields
* Generate hierarchical comparison reports
* Generate comparison summaries
* Save and manage comparisons
* Firebase authentication and data storage
* Responsive developer-focused interface

## How It Works

```text
Mock JSON
    │
    ▼
Schema Inference
    │
    ▼
Schema Normalization
    │
    ▼
Expected Schema ─────────────┐
                             │
                             ▼
                       Recursive
                       Comparison
                             ▲
                             │
API URL → Fetch API Response ┘
                             │
                             ▼
                    Comparison Tree
                             │
             ┌───────────────┼───────────────┐
             ▼               ▼               ▼
          Missing          Extra       Type Mismatch
             │               │               │
             └───────────────┼───────────────┘
                             ▼
                         Diff View
```

## Core Logic

The main comparison engine is implemented in:

```text
src/utils/ui2apiComparator.js
```

The application:

1. Infers a schema from the mock JSON.
2. Normalizes primitive, union, object, and array types.
3. Compares the expected schema against the actual API response recursively.
4. Identifies missing and extra fields.
5. Detects type mismatches.
6. Builds a hierarchical comparison tree.
7. Generates a summary of the comparison results.

Example:

```text
Expected:
{
  "id": number,
  "name": string
}

Actual:
{
  "id": "101",
  "email": "user@example.com"
}
```

The comparison identifies:

```text
id
  expected: number
  actual: string

name
  expected: string
  actual: missing

email
  actual: string
```

## Your Contribution

### Core Application Logic

I contributed to the **core logic of the application**, focusing on the processing and comparison pipeline.

Key contributions included:

* Implementing schema normalization for inferred JSON structures.
* Developing recursive comparison logic between expected schemas and actual API responses.
* Handling nested objects and arrays during comparison.
* Detecting missing, extra, and type-mismatched fields.
* Handling required and optional fields.
* Supporting primitive and union data types.
* Building hierarchical comparison results for nested JSON structures.
* Implementing comparison summary generation.
* Generating structured Markdown comparison reports.
* Adding safeguards for deeply nested JSON structures and edge cases.

The primary logic is organized into utility modules such as:

```text
src/utils/ui2apiComparator.js
src/utils/generateComparisonDict.js
src/utils/comparisonSummary.js
src/utils/generateMarkdownReport.js
```

## Tech Stack

### Frontend

* React
* Vite
* React Router
* Tailwind CSS
* Framer Motion
* Monaco Editor

### State & Data

* Redux Toolkit
* React Redux
* TanStack React Query
* Firebase
* Firestore
* Firebase Storage

### JSON & Comparison

* JSONHero Schema Infer
* JSON Schema
* Lodash ES

### UI Utilities

* Lucide React
* Sonner
* React Markdown

## Project Structure

```text
src/
├── components/
│   ├── dashboard/
│   ├── layout/
│   ├── schemaInfer/
│   ├── DiffView.jsx
│   ├── SchemaInferPlayground.jsx
│   └── ...
│
├── services/
│   └── ...
│
├── state/
│   ├── auth/
│   └── store.js
│
├── utils/
│   ├── ui2apiComparator.js
│   ├── generateComparisonDict.js
│   ├── generateMarkdownReport.js
│   ├── comparisonSummary.js
│   ├── formatTimestamp.js
│   └── ...
│
├── App.jsx
└── Router.jsx
```

## Installation

Clone the repository:

```bash
git clone https://github.com/KeerthanaGopal28/UI2API-.git
cd UI2API-
```

Install dependencies:

```bash
npm install
```

Start the development server:

```bash
npm run dev
```

The application will be available at the local Vite development URL.

## Example Use Case

A developer creates a mock JSON response while building a frontend.

Later, the backend API returns a different structure.

Instead of manually checking both responses, UI2API can compare them and highlight:

```text
✓ Matching fields

⚠ Missing fields
  user.profile.phone

⚠ Extra fields
  user.profile.address

⚠ Type mismatch
  user.age
  Expected: number
  Actual: string
```

This makes API contract differences easier to identify during frontend-backend integration.

## Comparison Statuses

| Status          | Meaning                                    |
| --------------- | ------------------------------------------ |
| `OK`            | Expected and actual data match             |
| `MISSING`       | Expected field is absent from API response |
| `EXTRA`         | API response contains an unexpected field  |
| `TYPE_MISMATCH` | Field exists but its data type differs     |

## Development

Build the application:

```bash
npm run build
```

Run linting:

```bash
npm run lint
```

Preview the production build:

```bash
npm run preview
```

## Future Improvements

* Support additional API response formats
* Add API authentication options
* Improve schema comparison visualization
* Add more advanced API contract validation
* Export comparison results in additional formats
* Add automated regression checks for API changes

## Author

**Keerthana Gopal**

GitHub: https://github.com/KeerthanaGopal28
