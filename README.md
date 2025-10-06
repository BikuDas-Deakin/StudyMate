# StudyMate

StudyMate is a web-based collaboration platform that allows students to create study groups, share learning resources, and collaborate in real time. The system provides a modular backend, responsive interface, and containerized deployment for easy setup and reproducibility.

## ⚙️ Project Overview

StudyMate enables peer-to-peer learning and group collaboration through shared study rooms, real-time chat, resource sharing, and productivity tools such as the Pomodoro timer. It is built with a lightweight Node.js architecture and designed for easy scaling and deployment using Docker and Jenkins CI/CD.

### Key Objectives

- Facilitate collaborative and structured study sessions
- Provide real-time communication and shared resources
- Maintain a modular, maintainable, and easily deployable codebase

## 🧩 Technology Stack

### Frontend
- **HTML5, CSS3, JavaScript**
- **Bootstrap 5** for responsive UI design

### Backend
- **Node.js and Express.js** – Core API and server
- **Socket.io** – Real-time messaging and room updates
- **Passport.js with JWT** – Secure authentication

### Database
- **MongoDB Atlas** (cloud-hosted)
- **Mongoose** for schema modeling and data access

### DevOps
- **Docker + Docker Compose** for containerized deployment
- **Jenkins** for CI/CD pipeline automation

### Testing
- **Jest** – Unit and integration testing
- **Cypress** – End-to-end testing suite

## 🚀 Features

- **Authentication & Authorization** – User registration, login, and JWT-based session management with role-based access for Admins and Members
- **Study Rooms & Collaboration** – Create or join rooms, share notes, and manage member access
- **Real-time Chat** – Persistent, room-specific chat using Socket.io
- **Pomodoro Timer** – Collaborative session timer with visual and audio notifications
- **Responsive Interface** – Mobile-friendly UI powered by Bootstrap
- **Containerized Deployment** – Backend and database run in Docker containers for easy setup
- **CI/CD Integration** – Jenkins pipeline automates build, test, and deployment stages

## 📁 Folder Structure

```
StudyMate/
│
├── backend/             # Node.js + Express backend
│   ├── controllers/     # Business logic and handlers
│   ├── models/          # Mongoose schemas
│   ├── routes/          # API route definitions
│   ├── middleware/      # Authentication, validation, roles
│   ├── utils/           # Helper utilities
│   └── app.js           # Server entry point
│
├── frontend/            # Static frontend resources
│   ├── public/          # HTML, CSS, JS, images
│   └── views/           # Static page templates
│
├── docker/              # Docker and Compose setup
│   ├── Dockerfile
│   └── docker-compose.yml
│
├── docs/                # Documentation (API, testing, design)
│   ├── api.md           # API endpoints and examples
│   ├── testing.md       # Test plans and results
│   ├── uiux.md          # Design decisions and wireframes
│   └── srs.md           # Software requirements specification
│
└── README.md
```

## ⚡ Getting Started

### Prerequisites

- **Node.js** v16+
- **npm** or **yarn**
- **Docker Desktop**
- **MongoDB Atlas URI**
- **Git**

### Local Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/BikuDas-Deakin/StudyMate.git
   cd StudyMate
   ```

2. **Install backend dependencies**
   ```bash
   cd backend
   npm install
   ```

3. **Create `.env` file in the backend directory**
   ```env
   PORT=5000
   MONGO_URI=<your-mongodb-atlas-uri>
   JWT_SECRET=<your-jwt-secret>
   NODE_ENV=development
   ```

4. **Run development server**
   ```bash
   npm run dev
   ```

5. **Access the app**
   ```
   http://localhost:5000
   ```

## 🐳 Docker Deployment

1. **Navigate to the docker directory**
   ```bash
   cd docker/
   ```

2. **Build and start containers**
   ```bash
   docker-compose build
   docker-compose up
   ```

3. **Access running services**
   - Backend: `http://localhost:5000`
   - MongoDB: `localhost:27017`

4. **Stop containers**
   ```bash
   docker-compose down
   ```

## 🧪 Testing

Run the following scripts from the `backend/` directory:

```bash
# Unit tests with Jest
npm test

# End-to-end tests with Cypress
npm run cypress:open
```

Test coverage includes authentication, CRUD operations, and socket-based chat functionality.

## 🔁 CI/CD Pipeline

StudyMate includes a Jenkins pipeline that automates:

- Source checkout from GitHub
- Docker image build and containerization
- Automated test execution
- Deployment to a containerized environment

Pipeline configuration can be found in the root `Jenkinsfile`.

## 👥 Team

**Project: StudyMate**

| Name | Role |
|------|------|
| Bisheshwar | Full Stack Developer / Project Lead |
| Anusha | Frontend Developer & UI/UX Designer |
| Mehakpreet Singh Sohal | Backend Developer & DevOps Engineer |

## 📚 Documentation

- `/docs/api.md` – API endpoints and sample requests
- `/docs/testing.md` – Test plans and results
- `/docs/uiux.md` – Design decisions and wireframes
- `/docs/srs.md` – Functional & non-functional requirements

## 🧠 Contribution Workflow

1. Work from the `dev` branch
2. Create a feature branch
   ```bash
   git checkout -b feature/<feature-name>
   ```
3. Develop, test, and commit changes
4. Open a Pull Request to `dev`
5. Merge into `main` after review and testing

## 🛠️ Tools & Resources

- **GitHub Repository**: [https://github.com/BikuDas-Deakin/StudyMate](https://github.com/BikuDas-Deakin/StudyMate)
- **Trello Board**: [StudyMate Project Board](https://trello.com/invite/b/68b7ef1e0722ebe79760e74d/ATTI0bc6f91b8f3d0256dd20099cbbb1c5e9E5E19FF6/studymate)

## 📞 Support

For issues or contributions:

- Check existing GitHub issues
- Open a new issue with clear details
- Contact team members via project communication channels

---

**Built with ❤️ by the StudyMate Team**
