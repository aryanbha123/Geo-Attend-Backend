# Geo Attend

Employee attendance system that checks people in with face recognition and records their geolocation.

![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![TensorFlow](https://img.shields.io/badge/TensorFlow.js-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![MUI](https://img.shields.io/badge/MUI-007FFF?style=for-the-badge&logo=mui&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)

## About

Geo Attend is a full-stack attendance app with a React client and an Express server. An employee opens the webcam, the browser matches their face against the photo they registered with (using face-api.js), and on a match it sends their latitude and longitude to the backend to mark check-in or check-out. Admins can look up attendance records by date.

## Features

**Client (`client/`)**

- Login and registration (username, email, password, role and a profile photo)
- Role-based routing for `Admin` and `Employee`, with protected routes
- **Face verification in the browser**: loads face-api.js models (SSD MobileNet v1, 68-point landmarks, face recognition) from `public/models`, builds a reference descriptor from the user's uploaded photo and matches it against the live webcam feed
- **Geolocation**: on a successful match, sends the user's coordinates to mark attendance or check-out
- Employee dashboard with camera controls, a calendar view of events and a colleagues list
- Admin dashboard with attendance records for a selected date
- Toast notifications (react-hot-toast, react-toastify)

**Server (`server/`)**

- Express app with CORS and cookie-parser, connecting to MongoDB through Mongoose
- Currently exposes only a health-check route on port `8000`

## Project Status

The client calls these backend endpoints: `/login`, `/logout`, `/register`, `/mark-attendance`, `/mark-checkout`, `/attendance/:date`, `/calendar/events`, `/calendar/delete-event/:id` and `/uploads/<username>.jpg`. They are not implemented in `server/index.js` yet, which only serves `GET /`. The client's base URL is hard-coded to `http://localhost:3000` in `client/src/AuthContext.jsx`.

## Tech Stack

- **Client:** React 18 (Create React App), React Router 6, face-api.js + TensorFlow.js, Material UI, Tailwind CSS, Framer Motion, react-calendar, Axios
- **Server:** Node.js, Express 4, Mongoose 8, jsonwebtoken, cookie-parser, dotenv

## Project Structure

```
client/
  public/models/        # face-api.js model weights
  src/
    App.jsx             # Routes
    AuthContext.jsx     # Auth state, login/logout, API base URL
    ModelContext.jsx    # face-api.js model loading
    auth/ProtectedRoute.jsx
    components/         # Login, Register
    pages/admin/        # Dashboard, Attendance, Sidebar
    pages/employee/     # Dashboard (face check-in), Calendar, List, Sidebar, Footer
server/
  index.js              # Express server
```

## Getting Started

**Prerequisites:** Node.js and npm, a MongoDB instance, and a browser with webcam and location access.

Server:

```bash
cd server
npm install
node index.js          # http://localhost:8000
```

Client:

```bash
cd client
npm install
npm start
```

### Environment Variables

Create `server/.env` with:

| Name | Description |
| --- | --- |
| `MONGO_DB_URI` | MongoDB connection string |

## API Endpoints

| Method | Endpoint | Description |
| --- | --- | --- |
| GET | `/` | Health check |

## Author

**Aryan Bhandari**: [GitHub](https://github.com/aryanbha123)
