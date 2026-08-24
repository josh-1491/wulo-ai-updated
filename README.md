# Pheli AI

Pheli AI is an AI-powered video generation platform that transforms simple text prompts into cinematic videos, advertisements, social media content, product videos, and creative stories.

## Features

* 🎬 **Text-to-Video** — Generate cinematic videos from natural-language prompts.
* 🖼️ **Image-to-Video** — Bring still images to life with AI-generated motion.
* 📢 **AI Ad Creation** — Create professional product and marketing videos.
* ⚡ **Fast Generation** — Turn ideas into videos with an intuitive AI workflow.
* 🎥 **HD Video** — Generate high-quality videos for digital content.
* 📥 **Video Downloads** — Download completed videos.
* 🔗 **Video Sharing** — Share generated videos.
* 🕘 **Generation History** — Keep track of previously generated videos.

---

# Tech Stack

## Frontend

* HTML5
* CSS3
* JavaScript
* Local Storage
* Fetch API

## Backend

The backend is responsible for:

* User authentication
* Video generation
* AI model requests
* Generation queues
* Video status tracking
* Video storage
* Credits and subscriptions

---

# Project Structure

```text
pheli-ai/
│
├── index.html
├── style.css
├── script.js
│
├── backend/
│   ├── server.js
│   │
│   ├── routes/
│   │   └── video.js
│   │
│   └── services/
│       └── video-generator.js
│
└── public/
    └── videos/
```

---

# Frontend Setup

Clone the project:

```bash
git clone YOUR_REPOSITORY_URL
cd pheli-ai
```

Run the project using a local development server:

```bash
npx serve .
```

Then open the local URL provided by the development server.

---

# Video Generator

Pheli AI accepts a text prompt describing the video the user wants to create.

Example:

```text
A cinematic luxury car driving through downtown Tokyo at night,
with neon lights reflecting across the wet streets. Slow camera
movement, realistic lighting, premium commercial style.
```

The frontend sends the request to:

```text
POST /api/generate-video
```

Example request:

```json
{
  "prompt": "A cinematic luxury car driving through Tokyo at night",
  "duration": "10 Seconds",
  "quality": "HD"
}
```

---

# Video Duration

Pheli AI supports configurable video durations.

```text
5 Seconds
10 Seconds
15 Seconds
30 Seconds
```

Actual duration availability depends on the selected AI video-generation model.

---

# Video Quality

Supported quality options:

```text
HD
Full HD
4K
```

Actual resolution availability depends on the AI video provider.

---

# Video Generation API

Pheli AI supports both immediate and asynchronous video generation.

## Immediate Generation

If the video is available immediately:

```json
{
  "videoUrl": "https://your-storage.com/videos/video123.mp4"
}
```

The frontend displays the completed video automatically.

---

## Asynchronous Generation

For longer generation jobs, the backend can return:

```json
{
  "jobId": "video_123456",
  "status": "processing"
}
```

The frontend then checks:

```text
GET /api/video-status/video_123456
```

While processing:

```json
{
  "status": "processing",
  "progress": 65
}
```

When complete:

```json
{
  "status": "completed",
  "videoUrl": "https://your-storage.com/videos/video123.mp4"
}
```

If generation fails:

```json
{
  "status": "failed",
  "message": "Video generation failed."
}
```

---

# Backend Architecture

Recommended workflow:

```text
User
  │
  ▼
Pheli AI Frontend
  │
  │ POST /api/generate-video
  ▼
Backend API
  │
  ▼
Authentication / Credits
  │
  ▼
Video Generation Queue
  │
  ▼
AI Video Model
  │
  ▼
Generated Video
  │
  ▼
Cloud Storage
  │
  ▼
Video URL
  │
  ▼
Pheli AI Video Player
```

The backend handles API credentials, authentication, generation jobs, storage, and billing.

---

# Security

Never expose AI provider API keys in frontend JavaScript.

Do not place secret credentials inside:

```text
index.html
script.js
style.css
```

Instead, store credentials on the backend.

Example:

```env
NODE_ENV=production

PORT=3000

VIDEO_API_KEY=your_secret_key

DATABASE_URL=your_database_url

STORAGE_BUCKET=your_bucket

AUTH_SECRET=your_auth_secret

STRIPE_SECRET_KEY=your_stripe_secret_key
```

Add `.env` to `.gitignore`:

```gitignore
.env
node_modules/
```

---

# Video History

The frontend can temporarily store generated video information using Local Storage.

Use:

```javascript
localStorage.getItem("pheliVideoHistory");
```

For production, video history should be stored in a database.

Example video record:

```json
{
  "id": "video_123",
  "userId": "user_456",
  "prompt": "A futuristic city at night",
  "videoUrl": "https://storage.example/video.mp4",
  "duration": 10,
  "status": "completed",
  "createdAt": "2026-08-22T20:00:00Z"
}
```

---

# Authentication

A production version should support:

* Sign up
* Login
* Logout
* Password recovery
* User profiles
* User video libraries

Every generated video should be associated with the authenticated user's account.

---

# Credits System

Pheli AI can use a credit-based system to manage video-generation costs.

Example:

```text
Free
5 generations

Creator
100 generations/month

Studio
Unlimited projects
```

Generation workflow:

```text
User
 ↓
Check Credits
 ↓
Enough Credits?
 ├── No → Upgrade
 │
 └── Yes
      ↓
 Generate Video
      ↓
 Deduct Credits
```

---

# AI Video Templates

Potential video templates include:

```text
Product Advertisement
Luxury Commercial
Real Estate
Travel
Fashion
Food Advertisement
Social Media Advertisement
Movie Trailer
Explainer Video
Product Showcase
```

---

# Advanced Video Controls

Future versions can include:

```text
Camera Movement
Camera Angle
Lighting
Visual Style
Character Description
Environment
Motion Strength
Seed
Negative Prompt
```

---

# Recommended API Endpoints

```text
POST   /api/auth/register
POST   /api/auth/login
POST   /api/auth/logout

GET    /api/user

GET    /api/videos
GET    /api/videos/:id
DELETE /api/videos/:id

POST   /api/generate-video
GET    /api/video-status/:jobId

POST   /api/upload-image

GET    /api/credits
POST   /api/credits/purchase

GET    /api/subscription
POST   /api/subscription
DELETE /api/subscription
```

---

# Error Handling

Pheli AI should handle:

```text
Invalid prompt
Insufficient credits
Generation failed
Generation timeout
AI provider unavailable
Network failure
Invalid video URL
Unsupported duration
Authentication failure
```

Example error response:

```json
{
  "error": "INSUFFICIENT_CREDITS",
  "message": "You do not have enough credits to generate this video."
}
```

All important validation must happen on the backend in addition to frontend validation.

---

# Production Considerations

Before launching publicly, consider adding:

* HTTPS
* Secure authentication
* Rate limiting
* Input validation
* API request logging
* Database backups
* Cloud video storage
* CDN delivery
* Background job processing
* Automatic video cleanup
* Payment processing
* Content moderation
* Abuse prevention
* Usage monitoring

---

# Development Roadmap

## Phase 1 — Frontend

* [x] Landing page
* [x] AI prompt interface
* [x] Video duration selector
* [x] Video quality selector
* [x] Generate button
* [x] Loading state
* [x] Video preview
* [x] Download button
* [x] Share button

## Phase 2 — Backend

* [ ] API server
* [ ] Authentication
* [ ] Video generation endpoint
* [ ] Generation queue
* [ ] Video status endpoint
* [ ] Cloud storage
* [ ] Database

## Phase 3 — AI Video

* [ ] Text-to-video
* [ ] Image-to-video
* [ ] AI advertisements
* [ ] Product video generation
* [ ] Video enhancement
* [ ] Cinematic video templates

## Phase 4 — Monetization

* [ ] Credits
* [ ] Subscriptions
* [ ] Stripe integration
* [ ] Usage limits
* [ ] Billing dashboard

## Phase 5 — Production

* [ ] Analytics
* [ ] Monitoring
* [ ] Rate limiting
* [ ] Content moderation
* [ ] CDN
* [ ] Production deployment

---

# License

Copyright © 2026 Pheli AI.

All rights reserved.

This project is proprietary unless otherwise specified by the project owner.
