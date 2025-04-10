# 🧾 New Collection - Account API Endpoints

A set of endpoints for user account management including registration, login, email verification, and logout.

---


## 📝 1. Register

**Method:** `POST`  
**URL:** `{{api_base_url}}/api/accounts/v2/register/`

### Body
```json
{
  "email": "user@proton.me",
  "password": "StrongPassword123!",
  "confirm_password": "StrongPassword123!",
  "terms_accepted": true
}
```
**Response**
```json
{
  "status": 201,
  "message": "User created successfully. Verification email sent.",
  "data": {
    "user": {
      "id": 1,
      "email": "user@proton.me",
      "verified": false,
      ...
    },
    "tokens": {
      "access": "<access_token>",
      "refresh": "<refresh_token>"
    }
  }
}
```

### 🔁 Edge Case: Already Registered User

If a user tries to register again using an email that already exists:

- **If the email exists and is not verified:**

  **Response:**
  ```json
  {
    "status": 200,
    "message": "User exists but email not verified. Verification email resent."
    }
  ```



### 🔒 Edge Case: User Already Verified

If the user is already registered **and verified**, trying to register again with the same email will return:

**Response:**
```json
{
    "status": 400,
    "message": "Registration failed.",
    "data": {
        "email": [
            "Email already exists"
        ]
    }
}
```


## ✅ 2. Email Verification

**Method:** `GET`  
**URL:** `{{api_base_url}}/api/accounts/v2/email-verify/?token=<jwt_token>`

### 🔹 Description
Verifies the email using the provided JWT token. If the token is valid and the user is not already verified, the account is marked as verified and a welcome email is sent. The user is then redirected to the login page.

### 🔸 Query Parameters

| Name  | Type   | Required | Description                        |
|-------|--------|----------|------------------------------------|
| token | string | ✅ Yes   | The email verification JWT token. |

---

### 🟢 Success Response (Redirect)
**Status:** `302 Found`  
Redirects to:  
`https://storyvord.io/auth/sign-in`

---

### 🔁 Already Verified
**Status:** `400 Bad Request`  
```json
{
  "message": "Email already verified"
}
```

## 🔐 3. Login

**Method:** `POST`  
**URL:** `{{api_base_url}}/api/accounts/v2/login/`

### Body
```json
{
  "email": "user@proton.me",
  "password": "Strongpassword123!"
}
```

### Description
Authenticates the user and returns an access token if credentials are valid.

---

## 🚪 4. Logout

**Method:** `POST`  
**URL:** `{{api_base_url}}/api/accounts/v2/logout/`

### Body
```json
{
  "email": "user@proton.me",
  "password": "StrongPassword123!"
}
```

### Description
Logs out the authenticated user.

---