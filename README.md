# Live Code Editor

A real-time collaborative code editor that allows multiple users to edit code simultaneously in the same room. Built with the MERN stack (minus MongoDB for now, focusing on in-memory state) and Socket.io for real-time communication.

## 🚀 Features & Solutions

- **Real-time Collaboration**: Solves the problem of remote pair programming by allowing multiple developers to type and see changes instantly.
- **Room-based Architecture**: Users can create private rooms to collaborate securely.
- **Syntax Highlighting**: Supports JavaScript syntax highlighting via CodeMirror.
- **Active User List**: Shows who is currently online in the room.

## 🛠️ Architecture & Logic

The application follows a standard **Client-Server** architecture powered by **Socket.io** for bidirectional event-based communication.

1.  **Frontend (Client)**:
    - Built with **React** and **Vite**.
    - Uses **CodeMirror** for the code editor interface.
    - Manages socket connections to listen for `CODE_CHANGE`, `JOINED`, and `DISCONNECTED` events.
2.  **Backend (Server)**:
    - Built with **Node.js** and **Express**.
    - Uses `socket.io` to maintain active connections/rooms `Map`.
    - Broadcasts code changes to all other sockets in the same room.

### Key Workflows

- **Joining a Room**:
    1.  User enters Room ID and Username.
    2.  Client emits `ACTIONS.JOIN`.
    3.  Server adds socket to the room and notifies others via `ACTIONS.JOINED`.
    4.  Client receives the current code state from an existing user (sync).
- **Coding**:
    1.  User types in the editor.
    2.  Client emits `ACTIONS.CODE_CHANGE`.
    3.  Server broadcasts this to `socket.in(roomId)`.
    4.  Other clients update their editor content.

## 💻 Running Locally

### Prerequisites
- Node.js (v14+)
- npm

### Steps

1.  **Install Server Dependencies**:
    ```bash
    npm install
    ```

2.  **Install Client Dependencies**:
    ```bash
    cd client
    npm install
    ```

3.  **Start the Server**:
    From the root directory:
    ```bash
    npm run server:dev
    ```
    This runs the Node server on port 5000 (default).

4.  **Start the Client**:
    Open a new terminal, navigate to `client`, and run:
    ```bash
    cd client
    npm run dev
    ```
    Access the app at `http://localhost:5173`.

> **Note**: The client connects to `http://localhost:5000` by default.

## 📦 Deployment

The application is configured to serve the frontend static files from the Node.js server.

### 1. Build the Frontend
Navigate to the `client` directory and build the React app:
```bash
cd client
npm run build
```
This generates the static files in `client/dist`.

### 2. Prepare the Server
The `server.js` (entry point `index.js`) is correctly configured to serve files from `client/dist`.
Ensure you are in the root directory and have installed dependencies:
```bash
npm install
```

### 3. Deploy
You can deploy this entire folder to any Node.js hosting provider (Render, Heroku, Railway, etc.).

**Start Command**: `npm start`
(This runs `node server.js`, which serves both the API and the React frontend).
