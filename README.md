# Lab CRUD API

## Setup

1. Install dependencies:
   ```sh
   npm install
   ```

2. Create a `.env` file:
   ```env
   DB_HOST=localhost
   DB_USER=root
   DB_PASSWORD=yourpassword
   DB_NAME=lab_auth
   PORT=3000
   ```

3. Initialize MySQL database:
   ```sql
   CREATE TABLE IF NOT EXISTS users (
   id INT AUTO_INCREMENT PRIMARY KEY,
   email VARCHAR(100) NOT NULL UNIQUE,
   password_hash VARCHAR(255) NOT NULL,
   full_name VARCHAR(120),
   role VARCHAR(30) DEFAULT 'student',
   created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

   CREATE TABLE IF NOT EXISTS revoked_tokens (
   id INT AUTO_INCREMENT PRIMARY KEY,
   jti VARCHAR(64) NOT NULL UNIQUE,
   expires_at DATETIME NOT NULL,
   revoked_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

```
4. Run the server:
```sh
npm run dev   # with nodemon
# or
npm start
```
   

Server runs at: [http://localhost:3000](http://localhost:3000)

## API Endpoints

**Sign-up**
- `POST {{baseUrl}}/auth/signup`

  {
  "email": "user1@example.com",
  "password": "Pass@1234",
  "full_name": "User One",
  "role": "student"
}

**Login**
- `POST {{baseUrl}}/auth/login`

  {
  "email": "user1@example.com",
  "password": "Pass@1234"
}

**Postman → Tests (save to environment): In you login script, add the code below**
```
if (pm.response.code === 200) {
  const data = pm.response.json();
  pm.environment.set("token", data.token);
}
```
**New request**
```
Bearer Token --> {{token}}

GET {{baseUrl}}/profile
Authorization: Bearer {{token}}
```
**Logout**
```
POST {{baseUrl}}/auth/logout
Authorization: Bearer {{token}}
```
