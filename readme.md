# Go Todo App API

A simple web API that allows you to create, update, delete, and view tasks that you need to do. The API is written in Go and uses MongoDB as the database.

## Endpoints

The API has four endpoints:

- `/api/task` (POST): Create a new task
- `/api/task` (GET): Get all tasks
- `/api/task?id={id}` (GET): Get a task by ID
- `/api/task` (PUT): Update a task by ID
- `/api/task` (DELETE): Delete a task by ID

## Request and Response Format

The API accepts and returns JSON data. The JSON schema for a task object is as follows:

```json
{
  "_id": string, // the unique identifier of the task
  "title": string, // the title of the task
  "completed": boolean, // the completion status of the task
  "created_at": string // the creation time of the task in RFC 3339 format
}
```

## Examples

Here are some examples of how to use the API with curl commands and the expected responses.

### Create a new task

Request:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"title": "Learn Go"}' http://localhost:8080/api/task
```

Response:

```json
{
  "InsertedID": "60ca0a9a8b9f7e4b8c6d0f3"
}
```

### Get all tasks

Request:

```bash
curl -X GET http://localhost:8080/api/task
```

Response:

```json
[
  {
    "_id": "60ca0a9a8b9f7e4b8c6d0f3",
    "title": "Learn Go",
    "completed": false,
    "created_at": "2021-08-12T18:43:50Z"
  },
  {
    "_id": "60ca0aa8b9f7e4b8c6d0f4",
    "title": "Write documentation",
    "completed": true,
    "created_at": "2021-08-12T18:44:08Z"
  }
]
```

### Get a task by ID

Request:

```bash
curl -X GET http://localhost:8080/api/task?id=60ca0a9a8b9f7e4b8c6d0f3
```

Response:

```json
{
  "_id": "60ca0a9a8b9f7e4b8c6d0f3",
  "title": "Learn Go",
  "completed": false,
  "created_at": "2021-08-12T18:43:50Z"
}
```

### Update a task by ID

Request:

```bash
curl -X PUT -H "Content-Type: application/json" -d '{"_id": "60ca0a9a8b9f7e4b8c6d0f3", "title": "Learn Go", "completed": true}' http://localhost:8080/api/task
```

Response:

```json
{
  "MatchedCount": 1,
  "ModifiedCount": 1,
  "UpsertedCount": 0,
  "UpsertedID": null
}
```

### Delete a task by ID

Request:

```bash
curl -X DELETE -H "Content-Type: application/json" -d '{"_id": "60ca0a9a8b9f7e4b8c6d0f3"}' http://localhost:8080/api/task
```

Response:

```json
{
  "DeletedCount": 1
}
```
