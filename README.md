# WhatsApp-First Authentication Boilerplate (React + Node.js)

A production-ready, frictionless WhatsApp OTP authentication boilerplate built for hackathons and rapid prototyping. Powered by **React (Vite)**, **Node.js/Express**, and the official **[Minimoth Node SDK](https://minimoth.dev)**.

---

## Features

- **WhatsApp-First Login**: Instant OTP delivery directly to user WhatsApp without SMS carrier latency or DND delivery drops.
- **Official Minimoth SDK**: Uses `@minimoth/sdk-node` (`MiniMoth`) for clean, secure OTP dispatch and verification.
- **Modern React Components**: Modular structure with Vite, Lucide icons, and responsive state handling:
  1. **Phone Input Screen**: Country code prefix, clean number input, and instant validation.
  2. **OTP Verification Screen**: 6-digit individual passcode inputs with auto-advance, backspace handling, paste support, and a 30s resend cooldown timer.
  3. **Authenticated Dashboard**: Shows verified phone number, Session ID, and copyable JWT tokens (`accessToken`, `refreshToken`) with properly proportioned controls.
- **Refined Aesthetics**: Deep dark slate glassmorphism, glowing emerald WhatsApp accents, micro-animations, loading spinners, and toast notifications.
- **Zero-Friction Dev Setup**: Run both the Express API and Vite React frontend with a single command (`npm run dev`).

---

## Project Structure

```text
minimoth/
├── .env.example              # Example environment variables
├── .env                      # Local environment variables (API Key & Port)
├── package.json              # Project scripts and dependencies
├── vite.config.mjs           # Vite config with React plugin & API proxy
├── server.js                 # Express backend with Minimoth SDK
├── index.html                # Vite React HTML entry
├── src/
│   ├── main.jsx              # React mounting root
│   ├── App.jsx               # Application controller & state machine
│   ├── index.css             # Refined CSS design system & micro-interactions
│   └── components/
│       ├── Header.jsx        # Branding badge, logo & setup alerts
│       ├── LoginScreen.jsx   # Phone input & send OTP flow
│       ├── VerifyScreen.jsx  # 6-digit OTP boxes, timer & auto-advance
│       ├── DashboardScreen.jsx # Verified session info, token copying & sign out
│       └── Toast.jsx         # Smooth sliding toast alerts
└── README.md                 # Setup instructions & documentation
```

---

## Quickstart Guide

### 1. Prerequisites
- **Node.js** v18 or higher installed on your machine.
- A **Minimoth** account & API key (Get one from [Minimoth Dashboard](https://minimoth.dev)).

### 2. Install Dependencies
```bash
npm install
```

### 3. Configure Your Environment Variables
Ensure `.env` contains your Minimoth API key:
```env
MINIMOTH_API_KEY=mm_live_xxxxxxxxxxxxxxxxxxxxxxxx
PORT=3000
```

### 4. Start the Application
Run the full-stack development environment:

```bash
# Starts both Express API (:3000) and Vite React app (:5173) concurrently:
npm run dev
```

Or build and serve in production mode:
```bash
# Build React bundle:
npm run build

# Start Express server (serves the built React app on port 3000):
npm start
```

Visit **[http://localhost:3000](http://localhost:3000)** (or `http://localhost:5173` during `npm run dev`) in your browser.

---

## API Reference

### 1. Send OTP
- **Endpoint**: `POST /api/send-otp`
- **Request Body**:
  ```json
  {
    "phoneNumber": "+919876543210"
  }
  ```
- **Response** (`200 OK`):
  ```json
  {
    "success": true,
    "message": "OTP sent successfully via WhatsApp",
    "otpId": "otp_abc123",
    "expiresAt": "2026-10-07T08:50:00.000Z"
  }
  ```

### 2. Verify OTP
- **Endpoint**: `POST /api/verify-otp`
- **Request Body**:
  ```json
  {
    "phoneNumber": "+919876543210",
    "otp": "123456"
  }
  ```
- **Response** (`200 OK`):
  ```json
  {
    "success": true,
    "message": "Authentication successful",
    "sessionId": "sess_xyz789",
    "identityId": "id_123",
    "tokens": {
      "accessToken": "eyJhbGciOi...",
      "refreshToken": "eyJhbGciOi..."
    }
  }
  ```
