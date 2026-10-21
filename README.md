# CompusHub — Course Management (React + Axios)

This project implements the React frontend described in the supplied laboratory guide: list courses, edit a course with `PUT`, delete a course with confirmation, refresh the table, and safely normalize values to prevent `course.code.trim is not a function`.

## Requirements

- Node.js 18 or newer
- Existing Spring Boot API running at `http://localhost:8080`
- API endpoints:
  - `GET /api/v1/courses`
  - `PUT /api/v1/courses/{id}`
  - `DELETE /api/v1/courses/{id}`

The backend is not included or rewritten, matching the assignment scope.

## Run the frontend

1. Extract the ZIP file.
2. Open a terminal in the extracted `CompusHub_React_Edit_Delete` folder.
3. Install dependencies:

   ```bash
   npm install
   ```

4. Start the React development server:

   ```bash
   npm run dev
   ```

5. Open `http://localhost:5173`.

Make sure the Spring Boot backend is running before using the course list. The backend must permit CORS requests from `http://localhost:5173`, including `GET`, `PUT`, `DELETE`, and `OPTIONS`.

## API URL configuration

By default, the app uses:

`http://localhost:8080/api/v1/courses`

To use a different API URL, copy `.env.example` to `.env` and edit `VITE_API_URL`. Restart the Vite server after changing environment variables.

## Expected JSON fields

The component expects the GET endpoint to return a JSON array, for example:

```json
[
  {
    "id": 101,
    "code": "IS-401",
    "title": "Advanced Enterprise Web Development",
    "credits": 3
  }
]
```

The PUT request sends `code` and `title` as strings and `credits` as a number. Confirm these names and types match your existing Spring Boot DTO/model.

## Features

- Course table with ID, code, title, credits, and action buttons
- Edit form prefilled from the selected row
- Update via Axios `PUT`
- Delete confirmation and Axios `DELETE`
- Success and readable error messages
- Loading, empty, and refresh states
- `String(value ?? "").trim()` normalization to avoid `.trim()` errors on numeric or null values

## Troubleshooting

- **Network error:** start the backend and check the API URL.
- **CORS error:** allow the Vite origin and the required HTTP methods in Spring Boot.
- **400 Bad Request:** compare the PUT JSON payload with the backend DTO and validation rules.
- **404 Not Found:** check endpoint mappings and course IDs.
- **405 Method Not Allowed:** verify that PUT and DELETE mappings exist.
- **Code loses a prefix:** the backend must store course codes as strings; React cannot restore characters already lost in the API response.

## Build check

Run `npm run build` to create a production build in `dist/`.
