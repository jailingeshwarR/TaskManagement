# Task Management API

## Project Structure
```plaintext
├── src/
│   ├── prisma/
│   │   ├── schema.prisma
│   ├── auth/
│   │   ├── auth.controller.ts
│   │   ├── auth.module.ts
│   │   ├── auth.service.ts
│   │   ├── dto/
│   │   │   ├── login.dto.ts
│   │   │   ├── register.dto.ts
│   │   ├── guards/
│   │   │   ├── jwt-auth.guard.ts
│   │   ├── strategies/
│   │   │   ├── jwt.strategy.ts
│   ├── tasks/
│   │   ├── tasks.controller.ts
│   │   ├── tasks.module.ts
│   │   ├── tasks.service.ts
│   │   ├── dto/
│   │   │   ├── create-task.dto.ts
│   │   │   ├── update-task.dto.ts
│   ├── prisma/
│   │   ├── prisma.module.ts
│   │   ├── prisma.service.ts
│   ├── app.module.ts
│   ├── main.ts
├── config/
│   ├── database.config.ts
├── test/
│   ├── auth/
│   │   ├── auth.controller.spec.ts
│   │   ├── auth.service.spec.ts
│   ├── tasks/
│   │   ├── tasks.controller.spec.ts
│   │   ├── tasks.service.spec.ts
├── .env
├── .env.example
├── .gitignore
├── nest-cli.json
├── package.json
├── README.md
├── tsconfig.build.json
├── tsconfig.json
```

---

## Overview
This project is a Task Management API built with [NestJS](https://nestjs.com/) and [Prisma ORM](https://www.prisma.io/) using MongoDB as the database. It provides APIs for user authentication and task management, allowing users to create, read, update, and delete tasks.

The project is deployed on [Vercel](https://vercel.com/) for easy access.

---

## Features
- **Authentication**: User registration and login with JWT-based authentication.
- **Task Management**: CRUD operations for tasks linked to authenticated users.
- **Database**: MongoDB with Prisma ORM for schema-based data modeling.

---

## Prerequisites
Ensure you have the following installed:
- [Node.js](https://nodejs.org/) (v16 or later recommended)
- [PNPM](https://pnpm.io/) (preferred package manager)
- [MongoDB](https://www.mongodb.com/) (local or cloud instance)
- [Vercel CLI](https://vercel.com/docs/cli) (for deployment)

---

## Project Setup

### 1. Clone the Repository
```bash
git clone https://github.com/jailingeshwarR/TaskManagement
cd task-management-api
```

### 2. Install Dependencies
Install dependencies using PNPM:
```bash
pnpm install
```

### 3. Configure Environment Variables
Create a `.env` file in the project root and add the following variables:
```env
DATABASE_URL=<your_mongodb_connection_url>
JWT_SECRET=<your_jwt_secret>
```
Ensure `DATABASE_URL` points to your MongoDB instance.

### 4. Generate Prisma Client
Run the following command to generate the Prisma client:
```bash
npx prisma generate
```

### 5. Run the Project Locally
Start the application in development mode:
```bash
pnpm start:dev
```
Access the API at `http://localhost:3000`.

---

## Deployment on Vercel

### 1. Install Vercel CLI
If not already installed, install the Vercel CLI globally:
```bash
npm install -g vercel
```

### 2. Login to Vercel
Authenticate with your Vercel account:
```bash
vercel login
```

### 3. Deploy the Project
Run the following command to deploy the project:
```bash
vercel
```

### 4. Configure Environment Variables
Go to the Vercel Dashboard, navigate to your project settings, and add the required environment variables (`DATABASE_URL` and `JWT_SECRET`) under **Environment Variables**.

### 5. Redeploy
Re-deploy the project to apply the environment variables:
```bash
vercel --prod
```

The deployed API will be accessible at the provided Vercel URL.

---

## API Endpoints

### **Authentication**
#### POST `/auth/register`
- **Body**:
  ```json
  {
    "email": "string",
    "password": "string"
  }
  ```
- **Response**:
  ```json
  {
    "id": "string",
    "email": "string"
  }
  ```

#### POST `/auth/login`
- **Body**:
  ```json
  {
    "email": "string",
    "password": "string"
  }
  ```
- **Response**:
  ```json
  {
    "access_token": "string"
  }
  ```

### **Tasks**
#### POST `/tasks`
- **Headers**: `Authorization: Bearer <token>`
- **Body**:
  ```json
  {
    "title": "string",
    "description": "string"
  }
  ```
- **Response**:
  ```json
  {
    "id": "string",
    "title": "string",
    "description": "string",
    "status": "pending"
  }
  ```

#### GET `/tasks`
- **Headers**: `Authorization: Bearer <token>`
- **Response**:
  ```json
  [
    {
      "id": "string",
      "title": "string",
      "description": "string",
      "status": "pending"
    }
  ]
  ```

#### PATCH `/tasks/:id`
- **Headers**: `Authorization: Bearer <token>`
- **Body**:
  ```json
  {
    "title": "string",
    "description": "string",
    "status": "string"
  }
  ```

#### DELETE `/tasks/:id`
- **Headers**: `Authorization: Bearer <token>`

---

## Technologies Used
- **Backend Framework**: NestJS
- **ORM**: Prisma
- **Database**: MongoDB
- **Deployment**: Vercel

---

## Troubleshooting

### Common Errors
1. **`PrismaClient` not found**:
   - Ensure Prisma Client is generated using `npx prisma generate`.
   - Include the `prisma/generated/client` folder in your deployment.

2. **Environment variables not found**:
   - Verify `DATABASE_URL` and `JWT_SECRET` are correctly set in Vercel project settings.

### Logs
Check Vercel build logs for detailed error messages during deployment.

---

## License
This project is licensed under the [MIT License](./LICENSE).

