# 🔐 Forgot Password Flow API

This API enables users to securely reset their password using email verification and token-based validation.

---

## 📩 1. Request Password Reset

**Method:** `POST`  
**URL:** `{{api_base_url}}/accounts/request-reset-password/`

### Headers
| Key    | Value              |
|--------|--------------------|
| Accept | application/json   |

### Body
```json
{
  "email": "user@example.com"
}
```

### Description
Sends a password reset link to the provided email address. The link contains a secure token and encoded user ID (`uidb64`) to verify the reset request.

---

## 🔗 2. Verify Reset Link

**Method:** `GET`  
**URL:** `{{api_base_url}}/accounts/reset-password/<uidb64>/<token>/`

### Headers
| Key    | Value              |
|--------|--------------------|
| Accept | application/json   |

### Description
Verifies the validity of the reset token and user ID. This endpoint is accessed when the user clicks the link in the reset password email. No request body is required.

---

## 🔄 3. Complete Password Reset

**Method:** `POST`  
**URL:** `{{api_base_url}}/accounts/reset-password-complete/`

### Headers
| Key    | Value              |
|--------|--------------------|
| Accept | application/json   |

### Body
```json
{
  "email": "user@example.com",
  "password": "NewPassword@123"
}
```

### Description
Finalizes the password reset process. A valid email and new password are required to complete the reset.

---

## 🔁 Example Flow

1. **User submits email** via the `request-reset-password` endpoint.
2. **User receives a link** with a URL like:
   ```
   {{api_base_url}}/accounts/reset-password/<uidb64>/<token>/
   ```
3. **User clicks the link**, and token verification happens via `GET` request.
4. **User submits a new password** via the `reset-password-complete` endpoint.

---

## 🛡️ Notes

- Ensure tokens are time-limited for security (e.g. valid for 15–30 minutes).
- Passwords should meet your security policy (e.g. min 8 characters, symbols, etc.).
- The `email` field is used as an additional verification step when submitting the new password.

---