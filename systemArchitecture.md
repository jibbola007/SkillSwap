SkillSwap System Architecture 

Overview

SkillSwap is a MERN-stack (MongoDB, Express, React, Node) web application that connects users based on skills they can offer and skills they need.  
Users can match, chat, and rate each other after completing a skill exchange.



Frontend

Stack:React.js + Tailwind CSS  
Responsibilities:
-Render landing page and user dashboards  
-Handle authentication (login/signup)  
-Display skill listings and match suggestions  
-Chat interface (real-time updates via Socket.io client)

Data Flow:

-Sends HTTP requests to backend (REST API) for user, skill, and message data  
-Listens for WebSocket events for live messaging



Backend

Stack: Node.js + Express.js  
Responsibilities:
-User authentication (JWT)  
-CRUD operations for skills and offers  
-Matching algorithm (based on skills offered ↔ skills needed)  
-WebSocket setup for real-time chat  
-Rating and feedback system

API Examples:
-`POST /api/auth/signup` – register user  
-`GET /api/skills/match/:userId` – fetch compatible users  
-`POST /api/chat/message` – send message  



Communication Flow

Frontend (React) ↔ Backend (Express REST API) ↔ MongoDB  
WebSocket channel (Socket.io) for real-time messaging.  

Flow Example:

1.User logs in → receives JWT token  
2.React fetches skill matches → displays suggestions  
3.When two users agree → backend creates an “offer” record  
4.Socket.io opens chat → messages saved in `messages` collection  
5.After completion → both users leave ratings  



Technical Feasibility

-MERN stack supports rapid prototyping.  
-Socket.io handles chat without external dependencies.  
-MongoDB’s document model is flexible for skill tagging.  
-Can scale horizontally (separate chat microservice later).  



Future Improvements

-Add video chat via WebRTC  
-Integrate in-app wallet (for optional paid services)  
-Recommendation engine using collaborative filtering  
-Mobile app version (React Native)

Database Layer

Database: MongoDB Atlas  
Collections:
-`users` → name, bio, skills_offered[], skills_needed[]  
-`offers` → senderId, receiverId, status (pending/accepted/completed)  
-`messages` → chatId, senderId, text, timestamp  
-`ratings` → userId, raterId, score, comment  

Indexes added for quick skill-based lookups.
