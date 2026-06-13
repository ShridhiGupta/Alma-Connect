# Alma Connect - Alumni Association Platform

A full-stack alumni networking platform built with the **MERN stack** to connect students, alumni, and institutions through communication, events, AI assistance, and career support.

---

## 🚀 Features

- 👤 Role-based system (Student / Alumni / Admin)
- 💬 Real-time chat (Socket.IO)
- 📹 Video calling (WebRTC)
- 📅 Event creation & participation
- 🤖 AI career guidance (OpenAI + Gemini)
- 💰 Fundraising & donations (Razorpay)
- 🔔 Notifications system
- 📄 Resume upload & parsing
- 🛠 Admin dashboard

---

## 🧠 Tech Stack

**Frontend:** React, Tailwind CSS, Bootstrap, Axios, Socket.IO Client  
**Backend:** Node.js, Express.js, MongoDB, Mongoose, JWT  
**Realtime:** Socket.IO, WebRTC  
**AI & Services:** OpenAI API, Gemini API, Razorpay  

---

## 🏗 Architecture
```
React Frontend → Express Backend → MongoDB
↕
Socket.IO (Realtime Chat & Calls)
↕
AI + Payment Services (OpenAI, Gemini, Razorpay)
```

---

## 📂 Project Structure

```
/api → Backend (Controllers, Routes, Models)
/client → Frontend (React UI)
/config → Database configuration
/middleware → Auth & security
```

---

## 🔐 Authentication

- JWT-based authentication
- bcrypt password hashing
- Role-based access control:
  - Student → basic access
  - Alumni → networking + mentorship + events
  - Admin → full control

---

## ⚙️ Setup

```bash
git clone <repo-url>
cd project

# Backend
cd api
npm install
npm start

# Frontend
cd client
npm install
npm start

```

## 🔑 Environment Variables
```
MONGO_URI=your_mongo_uri
JWT_SECRET=your_secret
OPENAI_API_KEY=your_key
GEMINI_API_KEY=your_key
RAZORPAY_KEY=your_key
```

## 📈 Future Scope
```
Microservices architecture
Redis caching
Mobile app (React Native)
Email & push notifications
CI/CD pipeline
Advanced analytics dashboard
```

## ⭐ Why This Project
```
Real-world SaaS-level system
Full-stack + real-time features
AI integration (industry relevant)
Scalable architecture design
Strong placement-ready project
```

## If you want next upgrade, I can also:
- 🔥 make it “FAANG-level README” (more impactful wording)
- 🧠 add system design diagram
- 🚀 convert this into portfolio project card
- 💼 write resume bullet points for this project
