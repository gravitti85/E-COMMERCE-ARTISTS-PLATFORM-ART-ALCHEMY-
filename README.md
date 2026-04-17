# Art Alchemy 🎨

> An e-commerce platform for artists — built for the Kenyan creative economy.

Art Alchemy is a full-stack web application that provides visual artists and musicians with a dedicated digital marketplace to showcase and sell artwork, upload music albums, manage events, and analyse their sales performance through an AI-powered dashboard. Buyers can browse, purchase artwork, RSVP to events, and track their order history.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [1. Start MongoDB](#1-start-mongodb)
  - [2. Start the Backend](#2-start-the-backend)
  - [3. Start the Frontend](#3-start-the-frontend)
  - [4. Seed the Database](#4-seed-the-database)
- [User Roles](#user-roles)
- [API Reference](#api-reference)
- [Environment Configuration](#environment-configuration)
- [Known Limitations](#known-limitations)
- [Future Work](#future-work)
- [Author](#author)

---

## Features

### For All Users
- Account registration with role selection (Buyer, Musician, Visual Artist)
- JWT-based authentication with BCrypt password hashing
- Browse and search artwork catalog with category filtering
- View event listings and RSVP with email confirmation
- Shopping cart and prototype-level checkout with order history

### For Artists (Musician & Visual Artist)
- List, edit, and delete artwork for sale
- Create, manage, and delete events
- AI-powered Artist Dashboard with sales analytics
  - Revenue over time (line chart)
  - Pieces sold per month (bar chart)
  - Top artworks by revenue (horizontal bar chart)
  - AI-generated sales insights via the Anthropic Claude API

### For Musicians Only
- Upload music albums with cover art and audio files
- Full tracklist management with audio streaming

---

## Tech Stack

| Layer | Technology | Version |
|---|---|---|
| Frontend Framework | React + TypeScript | 18.2.0 |
| Build Tool | Vite | 5.0.8 |
| Styling | SASS/SCSS | 1.70.0 |
| Routing | React Router DOM | 6.21.2 |
| Charts | Recharts | 2.x |
| Backend Framework | Spring Boot | 3.2.6 |
| Backend Language | Java (Eclipse Temurin) | 21 LTS |
| Security | Spring Security + JWT (jjwt) | 0.12.5 |
| Database | MongoDB | 8.2 |
| Database Client | mongosh | 2.8.1 |
| Build Tool (Backend) | Apache Maven | 3.9.14 |
| AI Integration | Anthropic Claude API | claude-sonnet-4 |
| Email Service | Spring Boot Starter Mail | — |

---

## Project Structure

```
4th Yr Projo with Changes/
│
├── art-alchemy-master/          ← Frontend (React + TypeScript)
│   ├── src/
│   │   ├── api/                 ← API fetch functions (users, art, cart, orders, events, albums)
│   │   ├── components/          ← Reusable UI components
│   │   │   ├── Header/          ← Navigation with role-aware links and Dashboard button
│   │   │   ├── ArtistDashboard/ ← AI sales analytics panel
│   │   │   ├── ArtListings/     ← Artwork masonry grid
│   │   │   ├── Landing/         ← Home page components
│   │   │   └── Profile/         ← User profile and order history
│   │   ├── pages/               ← Route-level page components
│   │   │   ├── Events.tsx
│   │   │   ├── Albums.tsx
│   │   │   ├── AlbumDetail.tsx
│   │   │   ├── Blog.tsx
│   │   │   ├── Checkout.tsx
│   │   │   ├── SignUp.tsx
│   │   │   └── SignIn.tsx
│   │   ├── styles/              ← Page-level SCSS stylesheets
│   │   ├── utils/
│   │   │   └── custom_types.ts  ← TypeScript type definitions
│   │   └── App.tsx              ← Root component and route definitions
│   ├── package.json
│   └── vite.config.ts
│
├── backend/                     ← Backend (Spring Boot)
│   ├── src/main/java/com/kamiri/artalchemy/
│   │   ├── controllers/         ← REST API controllers
│   │   ├── services/            ← Business logic layer
│   │   ├── repositories/        ← Spring Data MongoDB repositories
│   │   ├── models/              ← MongoDB document models
│   │   ├── dto/                 ← Data Transfer Objects
│   │   ├── security/            ← JWT filter and Spring Security config
│   │   └── config/              ← CORS and security configuration
│   ├── src/main/resources/
│   │   └── application.properties ← Database, JWT, mail, and file storage config
│   └── pom.xml
│
└── seed_data.js                 ← MongoDB seed script (8 artworks + 6 events)
```

---

## Prerequisites

Make sure the following are installed before running the project:

| Tool | Version | Verify With |
|---|---|---|
| Java (Eclipse Temurin) | 21 LTS | `java -version` |
| Apache Maven | 3.9.x | `mvn -version` |
| Node.js | 20.x | `node -version` |
| npm | 10.x | `npm -version` |
| MongoDB | 8.2 | Installed as Windows Service |
| mongosh | 2.8.1 | `mongosh --version` |

---

## Getting Started

> **Important:** Always run Command Prompt **as Administrator** (right-click → Run as administrator) to avoid permission errors with Java.

Follow these steps in order every time you want to run the project.

---

### 1. Start MongoDB

MongoDB must be running before the backend can start. Open a Command Prompt **as Administrator** and run:

```
net start MongoDB
```

Expected output:
```
The MongoDB service is starting.
The MongoDB service was started successfully.
```

To verify MongoDB is running:
```
mongosh
```

You should see the `test>` prompt. Type `exit` to close mongosh.

> **If MongoDB is already running**, the command will say "The requested service has already been started." That is fine — proceed to Step 2.

> **To stop MongoDB** when you are done:
> ```
> net stop MongoDB
> ```

---

### 2. Start the Backend

Open a **new** Command Prompt **as Administrator**. Navigate to the backend folder and start Spring Boot:

```
cd "C:\Users\Administrator\Desktop\4th Yr Projo with Changes\backend"
mvn spring-boot:run
```

The first time you run this, Maven will download dependencies (takes 2–5 minutes). Subsequent runs are much faster.

Wait until you see all three of these lines:

```
Found 6 MongoDB repository interfaces.
Tomcat started on port 8080 (http)
Started ArtAlchemyApplication in X.XXX seconds
```

**Leave this Command Prompt window open.** The backend must stay running while you use the application.

> **If you see** `CreateProcess error=5, Access is denied` — you forgot to run as Administrator. Close and reopen Command Prompt with right-click → Run as administrator.

> **If you see** `MongoSocketOpenException: Connection refused` — MongoDB is not running. Go back to Step 1.

---

### 3. Start the Frontend

Open **another** new Command Prompt (does not need to be Administrator). Navigate to the frontend folder and start Vite:

```
cd "C:\Users\Administrator\Desktop\4th Yr Projo with Changes\art-alchemy-master"
npm run dev
```

Wait until you see:

```
VITE v5.x.x  ready

  ➜  Local:   http://localhost:5173/art-alchemy
```

Open your browser and go to:
```
http://localhost:5173/art-alchemy
```

The application is now running.

> **If you see** `Cannot find module 'recharts'` — run `npm install recharts` first, then `npm run dev` again.

---

### 4. Seed the Database

> **Only do this once.** If you run the seed script a second time it will insert duplicate records.

This step populates the Artwork and Events pages with sample data for demonstration purposes.

**Step 4a — Open mongosh:**

Open a new Command Prompt and run:
```
mongosh
```

**Step 4b — Switch to the art_alchemy database:**
```
use art_alchemy
```

You should see: `switched to db art_alchemy`

**Step 4c — Run the seed file:**
```
load("C:/Users/Administrator/Desktop/4th Yr Projo with Changes/seed_data.js")
```

Expected output:
```
✅ Inserted 8 artwork pieces
✅ Inserted 6 events
🎉 Seed complete! Refresh the browser to see the data.
```

**Step 4d — Verify the data was inserted:**
```
db.art.countDocuments()
db.events.countDocuments()
```

Should return `8` and `6` respectively.

**Step 4e — Refresh the browser.** The Artwork and Events pages will now show real data.

---

#### Removing Seed Data (if you need to re-seed)

If you accidentally ran the seed script twice and have duplicates, clear the collections and re-seed:

```
use art_alchemy
db.art.deleteMany({})
db.events.deleteMany({})
load("C:/Users/Administrator/Desktop/4th Yr Projo with Changes/seed_data.js")
```

---

## User Roles

The platform has three user roles, selected during account registration:

| Role | Description | Key Permissions |
|---|---|---|
| **Buyer** | Art purchasers | Browse artwork, add to cart, checkout, RSVP to events, view order history |
| **Musician** | Music artists | Everything a Buyer can do + list artwork, upload albums, create/delete events, access AI Dashboard |
| **Visual Artist** | Visual arts creators | Everything a Buyer can do + list artwork, create/delete events, access AI Dashboard |

Role-based access is enforced at two levels:
- **Frontend:** UI elements (buttons, nav links, Dashboard) are shown or hidden based on role
- **Backend:** Spring Security `@PreAuthorize` annotations reject unauthorised API requests server-side

---

## API Reference

The backend REST API runs on `http://localhost:8080`.

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| POST | `/api/users/sign-up` | None | Register new user |
| POST | `/api/users/sign-in` | None | Login, returns JWT token |
| GET | `/api/art?page=&size=` | None | Paginated artwork listings |
| GET | `/api/art/:id` | None | Single artwork (increments view count) |
| POST | `/api/art` | Musician / Visual Artist | Create artwork listing |
| DELETE | `/api/art/:id` | Authenticated (owner) | Delete artwork |
| GET | `/api/cart/:userId` | Authenticated | Fetch user's cart |
| POST | `/api/cart/update` | Authenticated | Update cart contents |
| POST | `/api/orders` | Authenticated | Place order (checkout) |
| GET | `/api/orders/my` | Authenticated | User's order history |
| GET | `/api/events?page=&size=` | None | Paginated events listing |
| POST | `/api/events` | Musician / Visual Artist | Create event |
| DELETE | `/api/events/:id` | Musician / Visual Artist (owner) | Delete event |
| POST | `/api/events/:id/rsvp` | Authenticated | RSVP to event (sends email) |
| DELETE | `/api/events/:id/rsvp` | Authenticated | Cancel RSVP |
| GET | `/api/albums?page=&size=` | None | Paginated albums |
| POST | `/api/albums` | Musician only | Upload album (multipart) |
| DELETE | `/api/albums/:id` | Musician (owner) | Delete album |
| GET | `/api/files/covers/:filename` | None | Serve album cover image |
| GET | `/api/files/audio/:filename` | None | Stream audio track |

All protected endpoints require the header:
```
Authorization: Bearer <JWT_TOKEN>
```

---

## Environment Configuration

The backend is configured via `backend/src/main/resources/application.properties`.

```properties
# ── Server ──────────────────────────────────────
server.port=8080

# ── MongoDB ─────────────────────────────────────
spring.data.mongodb.uri=mongodb://localhost:27017/art_alchemy
spring.data.mongodb.database=art_alchemy

# ── JWT ──────────────────────────────────────────
app.jwt.secret=your-secret-key-here
app.jwt.expiration-ms=86400000

# ── CORS ─────────────────────────────────────────
app.cors.allowed-origins=http://localhost:5173,http://localhost:3000

# ── File Storage ─────────────────────────────────
app.upload.audio-dir=uploads/audio
app.upload.cover-dir=uploads/covers

# ── Email (optional — for RSVP confirmations) ────
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=YOUR_GMAIL_ADDRESS
spring.mail.password=YOUR_GMAIL_APP_PASSWORD
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
app.mail.from=YOUR_GMAIL_ADDRESS
```

> **Note:** Email configuration is optional for local development. If not configured, RSVP and order confirmation emails will silently fail without crashing the application.

The AI Dashboard requires an Anthropic API key added directly in:
`art-alchemy-master/src/components/ArtistDashboard/index.tsx`

```typescript
"x-api-key": "sk-ant-YOUR_KEY_HERE",
"anthropic-version": "2023-06-01",
"anthropic-dangerous-direct-browser-access": "true",
```

> **Security note:** Never commit real API keys to version control. For production, proxy the Anthropic API call through the Spring Boot backend instead.

---

## Known Limitations

1. **Payment is prototype-level** — card details are accepted by the checkout form but no live payment gateway (M-Pesa, Stripe) is connected. Orders are saved to the database but no real financial transaction occurs.
2. **Local deployment only** — the system runs on localhost and has not been deployed to a production server.
3. **AI Dashboard uses sample data** — the sales charts display seed/placeholder figures. Full integration with real order analytics requires a dedicated aggregation endpoint.
4. **Audio storage is local** — album audio files are saved to the server's local disk (`uploads/audio/`). A cloud storage provider such as AWS S3 or Cloudinary would be required for production.
5. **No mobile application** — the platform is web-only. A mobile app was explicitly excluded from the project scope.

---

## Future Work

- **M-Pesa Integration** — Safaricom Daraja API for local mobile money payments
- **Cloud Deployment** — Spring Boot backend on Railway/Render, React frontend on Vercel, MongoDB on Atlas
- **Real-Time Analytics** — Connect AI Dashboard charts to actual order data from MongoDB
- **Mobile Application** — React Native or Flutter app using the existing REST API
- **NFT Support** — Blockchain-based digital ownership certificates for artwork
- **Push Notifications** — Real-time alerts via Spring WebSocket

---

## Author

**Mahihu Collins Joseph**
Registration Number: SC211/1316/2020
Bachelor of Science in Information Technology
Murang'a University of Technology
Supervisor: Dr. Geoffrey Mariga
March 2026
