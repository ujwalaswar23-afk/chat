# ChatApp - WhatsApp Clone

A modern, real-time chat application built with React, Vite, Node.js, Socket.IO, and MongoDB. Features include user-to-user messaging, payment integration with PhonePe, and a WhatsApp-inspired UI.

## Features

- 🔐 **User Authentication** - Phone number-based login
- 💬 **Real-time Messaging** - Instant messaging with Socket.IO
- 💰 **Payment Integration** - Send payments via PhonePe gateway
- 📱 **Responsive Design** - Mobile-first, WhatsApp-inspired UI
- 🟢 **Online Status** - See who's online in real-time
- 📊 **Message History** - Persistent chat storage with MongoDB
- 🎨 **Modern UI** - Built with Tailwind CSS

## Tech Stack

### Frontend
- React 18
- Vite
- Tailwind CSS
- Socket.IO Client
- React Router DOM
- Lucide React (Icons)

### Backend
- Node.js
- Express.js
- Socket.IO
- MongoDB with Mongoose
- JWT Authentication

## Prerequisites

Before running this application, make sure you have the following installed:

- Node.js (v16 or higher)
- MongoDB (local installation or MongoDB Atlas)
- npm or yarn

## Installation & Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd web-chatting-app
```

### 2. Frontend Setup

```bash
# Install frontend dependencies
npm install

# Start the development server
npm run dev
```

The frontend will be available at `http://localhost:3000`

### 3. Backend Setup

```bash
# Navigate to server directory
cd server

# Install backend dependencies
npm install

# Start MongoDB (if running locally)
mongod

# Start the backend server
npm run dev
```

The backend will be available at `http://localhost:5000`

### 4. Environment Variables

Create a `.env` file in the `server` directory with the following variables:

```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/chatapp
JWT_SECRET=your_jwt_secret_key_here
NODE_ENV=development
```

## Usage

1. **Login**: Enter your name and phone number to create an account
2. **Start Chatting**: Click the "+" button to start a new chat with a phone number
3. **Send Messages**: Type and send real-time messages
4. **Send Payments**: Click the ₹ icon in the chat header to send payments
5. **Online Status**: See who's online in your chat list

## Payment Integration

This application includes a demo PhonePe payment integration. For production use:

1. Register with PhonePe for Business
2. Obtain API credentials
3. Replace the demo payment logic with actual PhonePe SDK integration
4. Implement proper security measures and transaction verification

## Project Structure

```
web-chatting-app/
├── src/
│   ├── components/
│   │   ├── Login.jsx
│   │   ├── ChatInterface.jsx
│   │   ├── ChatSidebar.jsx
│   │   ├── ChatWindow.jsx
│   │   └── PaymentModal.jsx
│   ├── context/
│   │   ├── AuthContext.jsx
│   │   └── SocketContext.jsx
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
├── server/
│   ├── models/
│   │   └── index.js
│   ├── server.js
│   └── package.json
├── package.json
├── vite.config.js
├── tailwind.config.js
└── README.md
```

## API Endpoints

### Socket Events

- `userJoin` - User joins the application
- `startChat` - Start a new chat with a phone number
- `sendMessage` - Send a message to a chat
- `getMessageHistory` - Retrieve message history for a chat
- `newMessage` - Receive new messages
- `chatList` - Receive updated chat list
- `onlineUsers` - Receive list of online users

### REST API

- `GET /api/health` - Health check endpoint

## Database Schema

### User
- name: String
- phoneNumber: String (unique)
- avatar: String
- isOnline: Boolean
- lastSeen: Date

### Chat
- participants: [ObjectId] (User references)
- lastMessage: String
- lastMessageTime: Date
- chatType: String (private/group)

### Message
- chatId: ObjectId (Chat reference)
- senderId: ObjectId (User reference)
- senderName: String
- content: String
- type: String (text/image/file/payment)
- timestamp: Date
- isRead: Boolean

### Payment
- senderId: ObjectId (User reference)
- recipientId: ObjectId (User reference)
- amount: Number
- transactionId: String (unique)
- status: String (pending/completed/failed/cancelled)
- paymentMethod: String (phonepe/card/upi)
- note: String

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Disclaimer

This is a demo application. The payment integration is simulated and should not be used for actual financial transactions without proper security implementation and compliance with financial regulations.

## Deployment

This project is now configured to be deployed as a single Node.js app that serves both the backend API/Socket.IO and the built React frontend.

### Build and Start (Production)

```bash
# Install dependencies (root). This also installs server dependencies via postinstall
npm install

# Build the frontend (Vite -> dist/)
npm run build

# Start the production server (serves API, Socket.IO and static frontend)
npm start
```

The server will bind to `PORT` (defaults to `5000`) and serve the SPA from `dist/`.

### Environment Variables

Set the following variables in your deployment environment (e.g., Render, Railway, AWS, etc.):

```
PORT=5000
MONGODB_URI=your-mongodb-connection-string
JWT_SECRET=your_jwt_secret_key_here
NODE_ENV=production

# Optional: Restrict allowed CORS/Socket.IO origins (comma-separated)
# Use this if your frontend is hosted on a separate origin
CLIENT_ORIGIN=https://your-frontend-domain.com,https://www.your-frontend-domain.com

# Optional: Force client to connect to a specific Socket.IO server URL
# By default, the client uses same-origin in production
VITE_SERVER_URL=https://your-backend-domain.com
```

### Notes

- In production, `server/server.js` serves the compiled frontend from `dist/` and provides an SPA fallback so client-side routing works.
- Socket.IO CORS is configured from `CLIENT_ORIGIN` (or `ALLOWED_ORIGINS`). If not set, it will allow all origins. Prefer setting it explicitly in production.
- The client Socket.IO connection is environment-aware: it connects to same-origin in production, or `http://localhost:5000` in development. You can override with `VITE_SERVER_URL`.

## Support

For support, email support@chatapp.com or create an issue in the repository.
