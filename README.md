#  Alma Connect — Alumni Association Platform

**Alma Connect** is a full-stack alumni association platform designed to bridge the gap between **students**, **alumni**, and **institutions**. Built as part of the **Smart India Hackathon (SIH)**, it provides a centralized hub for networking, mentorship, event management, fundraising, and AI-powered career guidance.

---

## 📑 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Prerequisites](#-prerequisites)
- [Installation & Setup](#-installation--setup)
- [Environment Variables](#-environment-variables)
- [Running the Application](#-running-the-application)
- [API Endpoints](#-api-endpoints)
- [User Roles](#-user-roles)
- [Screenshots](#-screenshots)
- [Contributing](#-contributing)
- [License](#-license)

---

##  Features

### 🔐 Authentication & Authorization
- User registration with role selection (Student / Alumni / Admin)
- Secure login with **JWT**-based authentication
- Role-based access control (RBAC) via middleware
- Password hashing with **bcrypt**

### 👤 User Profiles
- Detailed profiles with education, skills, experience, and current job
- **AI-powered resume parsing** — upload a PDF resume and auto-populate profile fields using OpenAI
- Follow / unfollow system to build your network
- User directory for browsing all registered members

### 💬 Real-Time Chat
- **Socket.IO**-powered instant messaging between users
- Private chat rooms with message persistence in MongoDB
- Users list sidebar to select and start conversations

### 📹 Video Calling
- Peer-to-peer video calls via **WebRTC** signaling through Socket.IO
- Join video rooms and connect with other users in real time

### 📅 Event Management
- Create and browse events (Hackathons, Seminars, TED Talks, Workshops)
- RSVP / attend events
- Event detail pages with attendee lists

### 💰 Donation & Fundraising
- Create fundraising campaigns (Student Aid, University, Event)
- Donate to campaigns with **Razorpay** payment integration
- Track campaign progress with target and current amount
- Donation confirmation and receipt tracking

### 🧭 AI-Powered Career Guidance
- Personalized career roadmaps generated using **OpenAI GPT**
- Input your education, skills, interests, and career goals
- Get actionable advice: diagnosis, roadmap, project ideas, networking actions, and resources
- Fallback advice when API is unavailable

### 🤖 AI Chatbot (Alma Connect Assistant)
- Conversational chatbot powered by **Google Gemini 2.5 Flash**
- Context-aware responses scoped to the Alma Connect platform
- Role-specific guidance for students, alumni, and admins
- Privacy-conscious — never stores sensitive user data

### 🔔 Notifications
- In-app notification system for event updates and platform activity
- Mark notifications as read

### 📊 Admin Dashboard
- View platform-wide statistics (total users, events, fundraises)
- User directory management

---

## 🛠 Tech Stack

| Layer        | Technology                                                                 |
|-------------|---------------------------------------------------------------------------|
| **Frontend** | React 19, React Router v6, Tailwind CSS, Bootstrap 5, Framer Motion, Lucide Icons |
| **Backend**  | Node.js, Express 5, Socket.IO                                            |
| **Database** | MongoDB with Mongoose ODM                                                 |
| **Auth**     | JSON Web Tokens (JWT), bcryptjs                                           |
| **AI/ML**    | OpenAI GPT (career guidance & resume parsing), Google Gemini (chatbot)   |
| **Payments** | Razorpay                                                                  |
| **Real-time**| Socket.IO (chat & video signaling)                                        |
| **File Upload** | Multer, pdf-parse                                                     |

---

## 📁 Project Structure

```
alumni-sih-master/
├── api/                        # Backend (Express.js server)
│   ├── config/
│   │   └── db.js               # MongoDB connection setup
│   ├── controllers/
│   │   ├── authController.js       # Register & login logic
│   │   ├── alumniController.js     # Profile, resume upload, follow/unfollow
│   │   ├── eventController.js      # Event CRUD operations
│   │   ├── chatController.js       # Chat message retrieval
│   │   ├── chatbot.controller.js   # Gemini AI chatbot
│   │   ├── donationController.js   # Campaign & Razorpay donation
│   │   ├── guidanceController.js   # AI career guidance (OpenAI)
│   │   ├── notificationController.js
│   │   └── adminController.js      # Admin dashboard stats
│   ├── middleware/
│   │   ├── authMiddleware.js       # JWT verification
│   │   └── adminMiddleware.js      # Admin role check
│   ├── models/
│   │   ├── User.js                 # User schema (student/alumni/admin)
│   │   ├── Event.js                # Event schema
│   │   ├── Message.js              # Chat message schema
│   │   ├── Donation.js             # Individual donation records
│   │   ├── DonationCampaign.js     # Fundraising campaign schema
│   │   ├── Notification.js         # Notification schema
│   │   └── Admin.js                # Admin stats schema
│   ├── routes/                 # Express route definitions
│   ├── server.js               # Entry point — Express + Socket.IO
│   ├── package.json
│   └── nodemon.json
│
├── client/                     # Frontend (React app)
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── AdminDashboard.js   # Admin analytics panel
│   │   │   ├── AlumniChatbot.js    # Gemini-powered chatbot widget
│   │   │   ├── Chat.js             # Real-time chat interface
│   │   │   ├── VideoCall.js        # WebRTC video calling
│   │   │   ├── UsersList.js        # User directory sidebar
│   │   │   ├── ResumeUpload.js     # PDF resume upload & parse
│   │   │   ├── Navigation.js       # Navbar component
│   │   │   ├── FundRequestManager.js
│   │   │   ├── FloatingChatWidget.js
│   │   │   └── ui/                 # Reusable UI components
│   │   ├── pages/
│   │   │   ├── Landing.js          # Public landing page
│   │   │   ├── Home.js             # Authenticated home page
│   │   │   ├── Login.js            # Login form
│   │   │   ├── Register.js         # Registration form
│   │   │   ├── Profile.js          # User profile editor
│   │   │   ├── UserProfile.js      # View other user's profile
│   │   │   ├── Events.js           # Event listing page
│   │   │   ├── EventDetails.js     # Single event details
│   │   │   ├── Fundraising.js      # Donation campaigns page
│   │   │   ├── Guidance.js         # AI career guidance page
│   │   │   ├── Notifications.js    # Notifications page
│   │   │   ├── Learnmore.js        # About / learn more page
│   │   │   └── Dashboard.js        # Dashboard page
│   │   ├── assets/             # Images, videos
│   │   ├── styles/             # CSS stylesheets
│   │   ├── hooks/              # Custom React hooks
│   │   ├── lib/                # Utility libraries
│   │   ├── utils/              # Helper functions
│   │   └── App.js              # Root component with routing
│   ├── package.json
│   ├── tailwind.config.js
│   └── postcss.config.js
│
└── .gitignore
```

---

## 📋 Prerequisites

Make sure you have the following installed on your system:

| Software    | Version      | Download Link                                      |
|-------------|-------------|---------------------------------------------------|
| **Node.js** | v18 or later | [nodejs.org](https://nodejs.org/)                 |
| **npm**     | v9 or later  | Comes with Node.js                                |
| **MongoDB** | v6 or later  | [mongodb.com](https://www.mongodb.com/try/download/community) |
| **Git**     | Latest       | [git-scm.com](https://git-scm.com/)              |

---

## ⚙ Installation & Setup

### 1. Clone the Repository

After Cloning Run this command ..
```bash
cd alumni-sih/alumni-sih-master
```

### 2. Install Backend Dependencies

```bash
cd api
npm install
```

### 3. Install Frontend Dependencies

```bash
cd ../client
npm install
```

### 4. Set Up MongoDB

Make sure MongoDB is running locally on `mongodb://localhost:27017`. The app will automatically create the `alumni-sih-db` database.

**Option A** — Run MongoDB locally:
```bash
mongod
```

**Option B** — Use MongoDB Atlas (cloud):
Update the `MONGO_URI` in your `.env` file with your Atlas connection string.

---

## 🔑 Environment Variables

Create a `.env` file inside the `api/` directory:

```bash
cd api
touch .env    # or create manually on Windows
```

Add the following variables:

```env
# Server
PORT=3000

# Database
MONGO_URI= MongoDB Connection String

# Authentication
JWT_SECRET=your_jwt_secret_here

# OpenAI (for resume parsing & career guidance)
OPENAI_API_KEY=your_openai_api_key_here

# Razorpay (for donation payments) — optional
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
```


---

## 🚀 Running the Application

### Start the Backend Server

```bash
cd api
npm run dev      # Uses nodemon for auto-reload
# OR
npm start        # Production mode
```

The API server starts at **`http://localhost:3000`**.

### Start the Frontend Dev Server

Open a **new terminal**:

```bash
cd client
npm start
```

The React app starts at **`http://localhost:3001`** (or the next available port).

### Quick Start (Both Servers)

You can run both servers simultaneously in separate terminals:

| Terminal 1 (Backend) | Terminal 2 (Frontend) |
|---------------------|----------------------|
| `cd api && npm run dev` | `cd client && npm start` |

---

## 📡 API Endpoints

### Authentication
| Method | Endpoint         | Description          | Auth Required |
|--------|-----------------|----------------------|:------------:|
| POST   | `/api/auth/register` | Register a new user   | ❌ |
| POST   | `/api/auth/login`    | Login & get JWT token | ❌ |

### Alumni / Users
| Method | Endpoint                     | Description                        | Auth Required |
|--------|-----------------------------|------------------------------------|:------------:|
| GET    | `/api/alumni/users`          | List all users                     | ✅ |
| GET    | `/api/alumni/:id`            | Get user profile by ID             | ✅ |
| PUT    | `/api/alumni/me`             | Update current user's profile      | ✅ |
| POST   | `/api/alumni/upload-resume`  | Upload & parse resume (PDF)        | ✅ |
| POST   | `/api/alumni/parse-resume`   | Parse resume without saving        | ❌ |
| POST   | `/api/alumni/follow/:id`     | Toggle follow/unfollow a user      | ✅ |

### Events
| Method | Endpoint              | Description              | Auth Required |
|--------|----------------------|--------------------------|:------------:|
| GET    | `/api/events`         | List all events           | ✅ |
| POST   | `/api/events`         | Create a new event        | ✅ |
| GET    | `/api/events/:id`     | Get event details         | ✅ |
| POST   | `/api/events/:id/attend` | RSVP to an event       | ✅ |

### Donations
| Method | Endpoint                      | Description                   | Auth Required |
|--------|------------------------------|-------------------------------|:------------:|
| GET    | `/api/donation/campaigns`     | List all campaigns             | ✅ |
| POST   | `/api/donation/campaigns`     | Create a new campaign          | ✅ |
| GET    | `/api/donation/campaigns/:id` | Get campaign details           | ✅ |
| POST   | `/api/donation/campaigns/:id/donate` | Initiate a donation     | ✅ |
| POST   | `/api/donation/confirm`       | Confirm payment                | ✅ |

### Career Guidance
| Method | Endpoint           | Description                       | Auth Required |
|--------|-------------------|-----------------------------------|:------------:|
| POST   | `/api/guidance`    | Get AI-generated career guidance   | ✅ |

### Chatbot
| Method | Endpoint          | Description                  | Auth Required |
|--------|------------------|------------------------------|:------------:|
| POST   | `/api/chatbot`    | Chat with the AI assistant   | ❌ |

### Notifications
| Method | Endpoint                | Description              | Auth Required |
|--------|------------------------|--------------------------|:------------:|
| GET    | `/api/notification`    | Get user notifications    | ✅ |
| PUT    | `/api/notification/:id`| Mark as read              | ✅ |

### Admin Dashboard
| Method | Endpoint              | Description               | Auth Required |
|--------|----------------------|---------------------------|:------------:|
| GET    | `/api/dashboard/stats`| Get platform statistics    | ✅ (Admin) |

---

## 👥 User Roles

| Role       | Capabilities                                                                                   |
|-----------|-----------------------------------------------------------------------------------------------|
| **Student** | View profiles, chat, video call, attend events, donate, get career guidance, use chatbot     |
| **Alumni**  | All student features + create events, create campaigns, mentor students                      |
| **Admin**   | User directory management, view platform stats, moderate content                              |

---


## 🤝 Contributing

Contributions are welcome! Here's how to get involved:

1. **Fork** the repository
2. **Create** a feature branch: `git checkout -b feature/amazing-feature`
3. **Commit** your changes: `git commit -m 'Add amazing feature'`
4. **Push** to the branch: `git push origin feature/amazing-feature`
5. **Open** a Pull Request

Please make sure to:
- Follow existing code style and conventions
- Update documentation for any new features
- Test your changes before submitting

---


## 🙏 Acknowledgments

- Built for **Smart India Hackathon (SIH) 2025**
- Powered by [OpenAI](https://openai.com/) and [Google Gemini](https://deepmind.google/technologies/gemini/)
- Payment processing by [Razorpay](https://razorpay.com/)
- Real-time communication via [Socket.IO](https://socket.io/)

---

<p align="center">
  Made with ❤️ by <strong>Team Alma Connect</strong>
</p>
#   S m a r t - A l u m n i - M a n a g e r  
 