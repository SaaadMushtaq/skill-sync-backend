# SkillSync Backend

A robust and secure backend API for the SkillSync application - a full-stack platform for skill-based job marketplace and professional networking.

## Features

- **User Authentication**: Secure user registration and login with JWT-based token authentication
- **Password Security**: Bcrypt-based password hashing for enhanced security
- **Job Management**: Create, read, update, and delete job postings
- **Role-based Access**: Protected routes with middleware authentication
- **Input Validation**: Request validation using express-validator
- **Database Integration**: MongoDB with Mongoose ODM for data persistence
- **CORS Support**: Cross-origin request handling for frontend integration
- **Request Logging**: HTTP request logging with Morgan

## Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js v5.2.1
- **Database**: MongoDB with Mongoose v9.3.3
- **Authentication**: JWT (JSON Web Tokens) & Bcrypt
- **Validation**: express-validator
- **Development**: Nodemon (live reload)
- **Middleware**: Morgan (request logging), CORS
- **Environment Management**: dotenv

## Project Structure

```
skill-sync-backend/
├── src/
│   ├── app.js                 # Express app configuration
│   ├── server.js              # Server entry point
│   ├── config/
│   │   └── db.js              # Database configuration
│   ├── controllers/
│   │   ├── authController.js  # Authentication logic (register, login)
│   │   └── jobController.js   # Job management logic (CRUD operations)
│   ├── middleware/
│   │   └── authMiddleware.js  # JWT verification & authentication
│   ├── models/
│   │   ├── User.js            # User schema and model
│   │   └── Job.js             # Job schema and model
│   └── routes/
│       ├── authRoutes.js      # Authentication endpoints
│       └── jobRoutes.js       # Job management endpoints
├── package.json               # Project dependencies
├── .env                       # Environment variables (not in repo)
└── README.md                  # This file
```

## Installation

### Prerequisites

- Node.js (v14 or higher)
- npm (v6 or higher)
- MongoDB (local instance or Atlas cloud database)

### Steps

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd skill-sync-backend
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Create environment file**

   ```bash
   cp .env.example .env
   ```

4. **Configure environment variables** (see Configuration section below)

## Configuration

Create a `.env` file in the root directory with the following variables:

```
# Server Configuration
PORT=5000
NODE_ENV=development

# Database Configuration
MONGODB_URI=mongodb://localhost:27017/skillsync
# OR for MongoDB Atlas:
# MONGODB_URI=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/skillsync

# JWT Configuration
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPIRE=7d

# CORS Configuration (Optional)
CORS_ORIGIN=http://localhost:3000
```

## Getting Started

### Development Mode

Run the server with hot-reload using Nodemon:

```bash
npm run dev
```

The server will start on `http://localhost:5000` and automatically restart when you make changes.

### Production Mode

Run the server in production mode:

```bash
npm start
```

## API Endpoints

### Authentication Routes (`/api/auth`)

| Method | Endpoint    | Description                  | Auth Required |
| ------ | ----------- | ---------------------------- | ------------- |
| POST   | `/register` | Register a new user          | No            |
| POST   | `/login`    | Login user and get JWT token | No            |

**Example Request:**

```bash
# Register
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"password123"}'

# Login
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"password123"}'
```

### Job Routes (`/api/jobs`)

| Method | Endpoint | Description    | Auth Required |
| ------ | -------- | -------------- | ------------- |
| GET    | `/`      | Get all jobs   | No            |
| GET    | `/:id`   | Get job by ID  | No            |
| POST   | `/`      | Create new job | Yes           |
| PUT    | `/:id`   | Update job     | Yes           |
| DELETE | `/:id`   | Delete job     | Yes           |

**Example Request:**

```bash
# Get all jobs
curl http://localhost:5000/api/jobs

# Create a job (requires authentication token)
curl -X POST http://localhost:5000/api/jobs \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <jwt_token>" \
  -d '{"title":"Senior Developer","description":"..."}'
```

## Models

### User Model

- `email` - Unique email address
- `password` - Bcrypt hashed password
- `name` - User full name
- `createdAt` - Account creation timestamp
- `updatedAt` - Last update timestamp

### Job Model

- `title` - Job title
- `description` - Job description
- `requirements` - Job requirements array
- `salary` - Salary range
- `location` - Job location
- `postedBy` - Reference to User who posted
- `createdAt` - Job posting timestamp
- `updatedAt` - Last update timestamp

## Authentication

The API uses JWT (JSON Web Token) for authentication. Protected routes require a valid JWT token in the `Authorization` header:

```
Authorization: Bearer <your_jwt_token_here>
```

### How to Get a Token

1. Register or login using the auth endpoints
2. You'll receive a JWT token in the response
3. Include this token in the `Authorization` header for protected routes
4. The token is valid for the duration specified in `JWT_EXPIRE` environment variable

## Error Handling

The API returns standard HTTP status codes and error messages:

- `200 OK` - Request successful
- `201 Created` - Resource created successfully
- `400 Bad Request` - Invalid request data
- `401 Unauthorized` - Missing or invalid authentication
- `404 Not Found` - Resource not found
- `500 Internal Server Error` - Server error

## Development Guidelines

### Running in Development

```bash
npm run dev
```

This will:

- Start the server with hot-reload
- Use Nodemon to watch for file changes
- Display request logs via Morgan middleware

### Debugging

- Check server logs in the terminal
- Use MongoDB Compass to inspect database data
- Verify credentials and JWT tokens in requests

## Dependencies

- **express** - Web framework
- **mongoose** - MongoDB ODM
- **bcrypt** - Password hashing
- **jsonwebtoken** - JWT authentication
- **express-validator** - Request validation
- **cors** - Cross-origin support
- **morgan** - HTTP logging
- **dotenv** - Environment variables
- **nodemon** - Development watch mode (dev only)

## License

ISC

## Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -m 'Add YourFeature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

## Support

For issues, questions, or suggestions, please open an issue in the repository.

## Author

SkillSync Development Team

---

**Last Updated**: April 2026
