# Task Manager API

A simple RESTful API built with Laravel that allows users to manage tasks. The API supports basic CRUD operations, validation, and additional features like filtering, pagination, and search.

## Features

- **CRUD Operations**: Create, Read, Update, Delete tasks
- **Task Filtering**: Filter tasks by status and due date
- **Pagination**: Paginate task listings
- **Search**: Search for tasks by title

## Requirements

- PHP >= 8.0
- Composer
- PostgreSQL
- Laravel 9

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/NewtonKamau/task_api.git
cd task-manager-api
```

### 2. Install Dependencies

Install the necessary dependencies with Composer:

```bash
composer install
```

### 3. Configure Environment Variables

Copy the `.env.example` to `.env`:

```bash
cp .env.example .env
```

Then, set up your database credentials in `.env`:

```env
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=task_manager
DB_USERNAME=your_pg_user
DB_PASSWORD=your_pg_password
```

### 4. Generate Application Key

```bash
php artisan key:generate
```

### 5. Run Migrations

Run the migrations to create the `tasks` table in the database:

```bash
php artisan migrate
```

### 6. Start the Server

Start the Laravel development server:

```bash
php artisan serve
```

The API will now be accessible at `http://127.0.0.1:8000`.

## API Endpoints

### Task Endpoints

| Method | Endpoint         | Description           |
| ------ | ---------------- | --------------------- |
| POST   | `/api/tasks`     | Create a new task     |
| GET    | `/api/tasks`     | Retrieve all tasks    |
| GET    | `/api/tasks/{id}` | Retrieve a specific task |
| PUT    | `/api/tasks/{id}` | Update a task        |
| DELETE | `/api/tasks/{id}` | Delete a task        |

### Example Requests

1. **Create a Task**: `POST /api/tasks`
    - Body: `{ "title": "Task Title", "description": "Task Description", "due_date": "YYYY-MM-DD" }`
  
2. **Get All Tasks**: `GET /api/tasks`
    - Query Parameters: 
      - `status` (optional, e.g., `pending` or `completed`)
      - `due_date` (optional, e.g., `YYYY-MM-DD`)
      - `search` (optional, searches by title)
      - `page` (optional, for pagination)

3. **Get a Specific Task**: `GET /api/tasks/{id}`

4. **Update a Task**: `PUT /api/tasks/{id}`
    - Body: `{ "title": "Updated Title", "status": "completed" }`

5. **Delete a Task**: `DELETE /api/tasks/{id}`

## Validation Rules

- `title`: required, unique, maximum length of 255 characters
- `description`: optional, string
- `status`: optional, either `pending` or `completed` (default: `pending`)
- `due_date`: required, must be a future date

## Bonus Features

1. **Task Filtering**: Filter tasks by `status` and/or `due_date`.
2. **Pagination**: Paginate tasks with `?page=n`.
3. **Search**: Find tasks by `title` using `?search=query`.

## Example CURL Requests

1. **Create a Task**:
    ```bash
    curl -X POST http://127.0.0.1:8000/api/tasks \
    -H "Content-Type: application/json" \
    -d '{"title": "New Task", "description": "Description here", "due_date": "YYYY-MM-DD"}'
    ```

2. **Get All Tasks**:
    ```bash
    curl http://127.0.0.1:8000/api/tasks
    ```

3. **Update a Task**:
    ```bash
    curl -X PUT http://127.0.0.1:8000/api/tasks/1 \
    -H "Content-Type: application/json" \
    -d '{"title": "Updated Task Title", "status": "completed"}'
    ```

4. **Delete a Task**:
    ```bash
    curl -X DELETE http://127.0.0.1:8000/api/tasks/1
    ```

## License

This project is licensed under the MIT License.

