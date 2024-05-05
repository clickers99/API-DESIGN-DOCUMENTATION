````markdown
# API Design for Forum App

## Core Entities:

1. **User:**

   - **Attributes:**
     - ID (unique identifier)
     - Username
     - Email
     - Password (encrypted)
     - Profile Information (e.g., name, bio, avatar, etc.)

2. **Thread:**

   - **Attributes:**
     - ID (unique identifier)
     - Title
     - Content
     - Author (User ID)
     - Creation Date
     - Last Updated Date

3. **Reply:**
   - **Attributes:**
     - ID (unique identifier)
     - Thread ID (parent thread)
     - Content
     - Author (User ID)
     - Creation Date
     - Last Updated Date

## API Endpoints:

### User Management:

#### Register User:

- **Method:** POST
- **Endpoint:** /api/users/register
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
````

- **Response (Success):**
  ```json
  {
    "success": true,
    "message": "User registered successfully"
  }
  ```
- **Response (Failed):**
  ```json
  {
    "success": false,
    "message": "Registration failed. Please check your input data"
  }
  ```

#### Log In User:

- **Method:** POST
- **Endpoint:** /api/users/login
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
    "success": true,
    "message": "Login successful",
    "token": "JWT_token"
  }
  ```
- **Response (Failed):**
  ```json
  {
    "success": false,
    "message": "Login failed. Invalid email or password"
  }
  ```

#### Update User Profile:

- **Method:** PUT
- **Endpoint:** /api/users/profile
- **Request Body:**
  ```json
  {
    "name": "Updated Name",
    "bio": "Updated bio",
    "avatar": "url/to/new_avatar.jpg"
  }
  ```
- **Headers:**
  ```
  { "Authorization": "Bearer JWT_token" }
  ```
- **Response (Success):**
  ```json
  {
    "success": true,
    "message": "Profile updated successfully"
  }
  ```
- **Response (Failed):**
  ```json
  {
    "success": false,
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
    "title": "Thread Title",
    "content": "Thread content"
  }
  ```
- **Headers:**
  ```
  { "Authorization": "Bearer JWT_token" }
  ```
- **Response (Success):**
  ```json
  {
    "success": true,
    "message": "Thread created successfully",
    "thread_id": "thread_id"
  }
  ```
- **Response (Failed):**
  ```json
  {
    "success": false,
    "message": "Thread creation failed. Please check your input data"
  }
  ```

#### Save/Bookmark Thread:

- **Method:** POST
- **Endpoint:** /api/threads/{thread_id}/save
- **Headers:**
  ```
  { "Authorization": "Bearer JWT_token" }
  ```
- **Response (Success):**
  ```json
  {
    "success": true,
    "message": "Thread saved/bookmarked successfully"
  }
  ```
- **Response (Failed):**
  ```json
  {
    "success": false,
    "message": "Thread save/bookmark failed. Thread not found or already saved"
  }
  ```

#### Unsave/Unbookmark Thread:

- **Method:** DELETE
- **Endpoint:** /api/threads/{thread_id}/save
- **Headers:**
  ```
  { "Authorization": "Bearer JWT_token" }
  ```
- **Response (Success):**
  ```json
  {
    "success": true,
    "message": "Thread unsaved/unbookmarked successfully"
  }
  ```
- **Response (Failed):**
  ```json
  {
    "success": false,
    "message": "Thread unsave/unbookmark failed. Thread not found or not saved"
  }
  ```

### Reply Management:

#### Create New Reply:

- **Method:** POST
- **Endpoint:** /api/threads/{thread_id}/replies
- **Request Body:**
  ```json
  {
    "content": "Reply content"
  }
  ```
- **Headers:**
  ```
  { "Authorization": "Bearer JWT_token" }
  ```
- **Response (Success):**
  ```json
  {
    "success": true,
    "message": "Reply added successfully",
    "reply_id": "reply_id"
  }
  ```
- **Response (Failed):**
  ```json
  {
    "success": false,
    "message": "Reply addition failed. Please try again later"
  }
  ```

#### Update Reply:

- **Method:** PUT
- **Endpoint:** /api/replies/{reply_id}
- **Request Body:**
  ```json
  {
    "content": "Updated reply content"
  }
  ```
- **Headers:**
  ```
  { "Authorization": "Bearer JWT_token" }
  ```
- **Response (Success):**
  ```json
  {
    "success": true,
    "message": "Reply updated successfully"
  }
  ```
- **Response (Failed):**
  ```json
  {
    "success": false,
    "message": "Reply update failed. Please try again later"
  }
  ```

#### Delete Reply:

- **Method:** DELETE
- **Endpoint:** /api/replies/{reply_id}
- **Headers:**
  ```
  { "Authorization": "Bearer JWT_token" }
  ```
- **Response (Success):**
  ```json
  {
    "success": true,
    "message": "Reply deleted successfully"
  }
  ```
- **Response (Failed):**
  ```json
  {
    "success": false,
    "message": "Reply deletion failed. Please try again later"
  }
  ```
