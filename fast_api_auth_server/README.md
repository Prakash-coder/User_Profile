This `README.md` file includes clear and complete instructions for setting up the project, running the application, and using the API endpoints, along with examples.
# FastAPI Auth Server

## Setup Instructions

1. **Clone the repository**:
    ```sh
    git clone <repo_url>
    cd fastapi-auth-server
    ```

2. **Create and activate a virtual environment**:
    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3. **Install dependencies**:
    ```sh
    pip install -r requirements.txt
    ```

4. **Setup PostgreSQL database** and update `.env` file with the connection details:
    ```dotenv
    SECRET_KEY=your-generated-secret-key
    DATABASE_URL=postgresql://user:password@localhost/dbname
    ```

5. **Run Alembic migrations**:
    ```sh
    alembic upgrade head
    ```

6. **Run the FastAPI application**:
    ```sh
    uvicorn app.main:app --reload
    ```

7. **Access the API documentation**:
    Open your web browser and navigate to `http://localhost:8000/docs` for Swagger UI or `http://localhost:8000/redoc` for ReDoc.

## API Endpoints

### `POST /api/v1/register-user`

Register a new user.

**Request Body**:
- `name` (required): Name of the user.
- `email` (required): Email of the user.
- `location` (required): Location of the user.
- `about` (optional): A short bio of the user.
- `password` (required): Password for the user account.

**Response**:
- The newly created user with their `id`, `name`, `email`, `location`, and `about`.

**Example Request**:
```sh
curl -X POST "http://localhost:8000/api/v1/register-user" -H "Content-Type: application/json" -d '{
    "name": "John Doe",
    "email": "john.doe@example.com",
    "location": "New York",
    "about": "A short bio",
    "password": "yourpassword"
}'
curl -X POST "http://localhost:8000/api/v1/auth/login" -d 'username=john.doe@example.com&password=yourpassword'
curl -X POST "http://localhost:8000/api/v1/auth/refresh-token" -H "Content-Type: application/json" -d '{
    "refresh_token": "your-refresh-token"
}'
curl -X GET "http://localhost:8000/api/v1/me" -H "Authorization: Bearer your-access-token"
```


