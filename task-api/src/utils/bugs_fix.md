# Bugs

## 1. POST `/tasks` -- Invalid Date Validation

### Current Behaviour

-   `dueDate` accepts any numeric value if it is not `null`.
-   Invalid date formats are accepted instead of being rejected.

### Expected Behaviour

-   `dueDate` must only accept a valid date format (for example,
    ISO-8601).
-   If an invalid date is provided, the API should return:

``` http
HTTP/1.1 400 Bad Request
```

with an appropriate validation error message.

------------------------------------------------------------------------

## 2. GET `/tasks?limit=`

### Current Behaviour

-   The `limit` query parameter has no effect.

### Expected Behaviour

-   The API should respect the supplied `limit` value and return at most
    that number of tasks.

------------------------------------------------------------------------

## 3. PUT `/tasks/:id` -- Protected Fields Can Be Updated

### Current Behaviour

The following fields can currently be modified: - `id` - `createdAt` -
`completedAt`

### Expected Behaviour

These fields should be read-only and must not be updatable: - `id` -
`createdAt` - `completedAt`

Attempting to modify them should return:

``` http
HTTP/1.1 400 Bad Request
```

or

``` http
HTTP/1.1 403 Forbidden
```

depending on the API design.

------------------------------------------------------------------------

## 4. PUT `/tasks/:id` -- Invalid Date Validation

### Current Behaviour

-   Date fields accept arbitrary numeric or alphanumeric values.

### Expected Behaviour

-   All date fields should be validated using the same rules as task
    creation.
-   Invalid date formats should return:

``` http
HTTP/1.1 400 Bad Request
```

------------------------------------------------------------------------

## 5. PUT `/tasks/:id` -- Status Update Rules

### Current Behaviour

-   `status` can be updated directly through the update endpoint.

### Expected Behaviour

-   `status` should not be directly editable if task completion is
    intended to be handled exclusively through:

```{=html}
<!-- -->
```
    PATCH /tasks/:id/complete

This preserves a single source of truth for task completion and prevents
inconsistent task states.
