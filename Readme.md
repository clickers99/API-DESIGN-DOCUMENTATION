
# API Design for Forum App
- **Requirement/User Stories:**
   - As a user, I want to be able to Register
   - As a user, I want to be able to Log In
   - As a user, I want to be able to Create new Thread
   - As a user, I want to be able to Create new Reply (on a Thread)
   - As a user I want to be able to Update my Personal profile
   - As a user, I want to be able to Save/Bookmark Threads
   - As a user, I want to be able to UnSave/UnBM Threads

## Core Entities:

1. **User:**

   - **Attributes:**
     - Username : String,required
     - Email : String,required
     - Password : String,required
     - Profile Information :
         - Name: String (opsional)
         - Bio: String (opsional)
         - Avatar: String (opsional, URL atau path ke file gambar)

2. **Thread:**

   - **Attributes:**
     - Title : String,required
     - Content : String,required
     - UserId : String,required
     - Creation Date (created_at) : DateTime,required
     - Last Updated Date (updated_at) : DateTime,required

3. **Reply:**
   - **Attributes:**
     - Thread ID (parent thread) : String,required
     - Content : String,required
     - UserId : String,required
     - Creation Date (created_at) : DateTime,required
     - Last Updated Date (updated_at) : DateTime,required

4. **Bookmark:**

   - **Attributes:**
     - UserID: String (required)
     - ThreadID: String (required)
     - Creation Date (created_at): DateTime (required)

## API Endpoints:

### User Management:

#### Register User:

- **Method:** POST
- **Endpoint:** /api/register
- **Request Body:**
  ```json
  {
    "username": "example_user",
    "email": "user@example.com",
    "password": "password123",
    "profile": {
      "name": "John Doe",
      "bio": "Lorem ipsum",
      "avatar": "url/to/avatar.jpg"
    }
  }
  ```

- **Response (Success):**
  ```json
  {
    "status": 200,
    "message": "User registered successfully",
    "data": {
      "user_id": "123",
      "username": "example_user",
      "email": "user@example.com",
      "profile": {
        "name": "John Doe",
        "bio": "Lorem ipsum",
        "avatar": "url/to/avatar.jpg"
      }
    }
  }
  ```
- **Response (Failed):**
  ```json
  {
    "status": 400,
    "message": "Registration failed. Please check your input data"
  }
  ```

#### Log In User:

- **Method:** POST
- **Endpoint:** /api/login
- **Request Body:**
  ```json
  {
    "email": "user@example.com",
    "password": "password123"
  }
  ```
- **Response (Success):**
  ```json
  {
    "status": 200,
    "message": "Login successful",
    "data": {
      "user_id": "123",
      "username": "example_user",
    }
  }
  ```
- **Response (Failed):**
  ```json
  {
    "status": 401,
    "message": "Login failed. Invalid email or password"
  }
  ```

#### Update User Profile:

- **Method:** PATCH
- **Endpoint:** /api/users/:userId
- **Request Body:**
  ```json
  {
    "name": "Updated Name",
    "bio": "Updated bio",
    "avatar": "url/to/new_avatar.jpg"
  }
  ```
- **Response (Success):**
  ```json
  {
    "status": 200,
    "message": "Profile updated successfully",
    "data": {
      "user_id": "123",
      "username": "example_user",
      "profile": {
        "name": "Updated Name",
        "bio": "Updated bio",
        "avatar": "url/to/new_avatar.jpg"
      }
    }
  }
  ```
- **Response (Failed):**
  ```json
  {
    "status": 403,
    "message": "Profile update failed. Please try again later"
  }
  ```

### Thread Management:

#### Create New Thread:

- **Method:** POST
- **Endpoint:** /api/threads
- **Request Body:**
  ```json
  {
    "user_id": "User"
    "title": "Thread Title",
    "content": "Thread content"
  }
  ```
- **Response (Success):**
  ```json
  {
    "status": 200,
    "message": "Thread created successfully",
    "data": {
      "thread_id": "thread_id",
      "title": "Thread Title",
      "content": "Thread content",
      "user_id": "123",
      "creation_date": "2024-05-07T12:00:00Z",
      "last_updated_date": "2024-05-07T12:00:00Z"
    }
  }
  ```
- **Response (Failed):**
  ```json
  {
    "status": 400,
    "message": "Thread creation failed. Please check your input data"
  }
  ```

#### Save/Bookmark Thread:

- **Method:** POST
- **Endpoint:** /api/bookmarks

- **Request Body:**
  ```json
  {
    "user_id": "User",
    "thread_id": "thread_id"
  }
  ```
- **Response (Success):**
  ```json
  {
    "status": 200,
    "message": "Thread saved/bookmarked successfully"
  }
  ```
- **Response (Failed):**
  ```json
  {
    "status": 404,
    "message": "Thread save/bookmark failed. Thread not found or already saved"
  }
  ```

#### Unsave/Unbookmark Thread:

- **Method:** DELETE
- **Endpoint:** /api/bookmarks/:bookmarkId

Response (Success):\*\*

```json
{
  "status": 200,
  "message": "Thread unsaved/unbookmarked successfully"
}
```

- **Response (Failed):**
  ```json
  {
    "status": 404,
    "message": "Thread unsave/unbookmark failed. Thread not found or not saved"
  }
  ```

### Reply Management:

#### Create New Reply Thread:

- **Method:** POST
- **Endpoint:** /api/replies
- **Request Body:**
  ```json
  {
    "user_id" : "User"
    "author_id" : "Author"
    "thread_id" "Thread Id"
    "content": "Reply content"
  }
  ```
- **Response (Success):**
  ```json
  {
    "status": 200,
    "message": "Reply added successfully",
    "data": {
      "user_id" : "john"
      "reply_id": "Nice",
      "thread_id": "Devscale Bootcamp,
      "content": "Reply content",
      "author_id": "arthur",
      "creation_date": "2024-05-07T12:00:00Z",
      "last_updated_date": "2024-05-07T12:00:00Z"
    }
  }
  ```
- **Response (Failed):**
  ```json
  {
    "status": 400,
    "message": "Reply addition failed. Please try again later"
  }
  ```
