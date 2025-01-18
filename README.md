# User Management API

This project provides a User Management API built with FastAPI, supporting features such as creating, updating, deleting user profiles, finding potential matches, and validating email addresses.

## Features

1. **Create User**:
   - Endpoint: `POST /users/`
   - Description: Allows the creation of a new user.
   - Request Body:
     ```json
     {
       "name": "John Doe",
       "age": 25,
       "gender": "Male",
       "email": "johndoe@example.com",
       "city": "New York",
       "interests": ["coding", "reading"]
     }
     ```

2. **Read Users**:
   - Endpoint: `GET /users/`
   - Description: Fetch a paginated list of users.
   - Query Parameters:
     - `skip`: Number of records to skip.
     - `limit`: Maximum number of records to return.

3. **Read Single User**:
   - Endpoint: `GET /users/{user_id}`
   - Description: Fetch a single user by their unique ID.

4. **Update User**:
   - Endpoint: `PUT /users/{user_id}`
   - Description: Update details of an existing user.
   - Request Body (Partial updates supported):
     ```json
     {
       "name": "John Smith",
       "city": "San Francisco"
     }
     ```

5. **Delete User**:
   - Endpoint: `DELETE /users/{user_id}`
   - Description: Deletes a user profile by ID.

6. **Find Matches**:
   - Endpoint: `GET /users/{user_id}/matches`
   - Description: Finds potential matches for a user based on profile information (e.g., matching email domains).

7. **Email Validation**:
   - Added validation for the `email` field in all user-related schemas using `pydantic.EmailStr`.
   - Ensures only valid email addresses can be used in user profiles.

## Schemas

### UserBase
Fields:
- `name` (str): Name of the user.
- `age` (int): Age of the user.
- `gender` (str): Gender of the user.
- `email` (EmailStr): Validated email address.
- `city` (str): City where the user resides.
- `interests` (List[str]): List of user interests.

### UserCreate
- Inherits from `UserBase`.
- Used for creating new users.

### User
- Inherits from `UserBase`.
- Includes `id` (int): Unique identifier for a user.
- ORM configuration enabled using `orm_mode`.

## Setup Instructions

1. Clone the repository.
2. Install dependencies:
   ```bash
   pip install fastapi uvicorn sqlalchemy pydantic
   ```
3. Run the development server:
   ```bash
   uvicorn main:app --reload
   ```
4. Access the API documentation at:
   - Swagger UI: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
   - ReDoc: [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

## Example Requests

### Create User
```bash
curl -X POST "http://127.0.0.1:8000/users/" \
-H "Content-Type: application/json" \
-d '{
  "name": "Jane Doe",
  "age": 30,
  "gender": "Female",
  "email": "janedoe@example.com",
  "city": "Los Angeles",
  "interests": ["traveling", "cooking"]
}'
```

### Update User
```bash
curl -X PUT "http://127.0.0.1:8000/users/1" \
-H "Content-Type: application/json" \
-d '{
  "city": "Seattle"
}'
```

### Delete User
```bash
curl -X DELETE "http://127.0.0.1:8000/users/1"
```

### Find Matches
```bash
curl -X GET "http://127.0.0.1:8000/users/1/matches"
```

## Notes
- This project includes basic email validation and a simple matching algorithm based on email domains. Extend the matching logic as needed for your use case.
- The database schema and models should align with the provided API functionality.
