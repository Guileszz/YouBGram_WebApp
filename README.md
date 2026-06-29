# YouBGram — High-Performance AI Social Media PWA

YouBGram is a modern, SEO-optimized, Progressive Web App (PWA) designed for AI developers and coding communities. It features a custom React frontend served by a robust Node.js/Express backend with dynamic SEO rendering.

## 🛠 Tech Stack

- **Frontend**: React 18 (Vite), TailwindCSS-inspired custom CSS, Framer Motion.
- **Backend**: Node.js, Express.
- **Database**: SQLite3 (chosen for high performance on VPS/CPanel).
- **PWA**: Custom Service Workers, Web App Manifest.
- **SEO**: Server-side Dynamic Meta Injection.

---

## 📁 Directory Structure & File Usage

### 🌐 Root (Full-Stack Management)

- **`server.js`**: The orchestrator. Handles static file serving, **Dynamic SEO Injection** (injects meta tags into HTML based on DB data), Sitemap generation (`/sitemap.xml`), and Robots.txt.
- **`config.js`**: Centralized configuration for storage paths, security tokens, and server settings.
- **`.env`**: Sensitive credentials (JWT secrets, API keys).
- **`prd.md`**: Product Requirements Document (the original project vision).

### 🖥 `client/` (Frontend - React SPA)

- **`src/App.jsx`**: Main routing logic and global Auth Guards.
- **`src/components/PWAHandler.jsx`**: Manages installation prompts and notification permissions without being intrusive.
- **`src/components/Layout.jsx`**: The main UI shell (Sidebar, Navigation). Includes safety checks to prevent UI freezing on logout.
- **`public/sw.js`**: Service Worker for background notifications and PWA features.
- **`public/manifest.json`**: Defines the "Native App" identity for Android/iOS.

### ⚙️ Backend Logic

- **`db/database.js`**: Database schema definition and high-level query helpers (e.g., `findUserByUsername`, `getPostById`).
- **`routes/`**:
  - `api/v1/auth.js`: Registration, Login, and Profile management.
  - `api/v1/social.js`: Posts, Reels, Likes, and Comments logic.
  - `admin/`: Admin-specific dashboard and moderation APIs.
- **`controllers/`**: Contains the actual business logic for each route to keep the codebase clean.
- **`middleware/`**: Contains `auth.js` for JWT verification and session safety.
- **`jobs/`**: Background tasks like `cleanup.js` for deleting old notifications or temporary files.

### 💾 Data & Persistence (CRITICAL)

- **`data/app.db`**: The live SQLite database file. **DO NOT OVERWRITE DURING UPDATES.**
- **`storage/`**:
  - `avatars/`: User profile pictures.
  - `posts/`: Uploaded images and videos.
  - `ads/`: Promotional banners.
  - **DO NOT OVERWRITE THESE DIRECTORIES DURING UPDATES.**

---

## 🚀 Deployment & Updates

### 📥 Initial Deployment

1. Upload the ZIP.
2. Extract to `public_html`.
3. Set up Node.js app in CPanel pointing to `server.js`.
4. Run `npm install`.

### 🔄 Updating Without Data Loss

When pushing new features, follow this "Clean Update" protocol:

1. **Exclude** the `data/` and `storage/` folders from your update package.
2. Replace `server.js`, `dist/`, `routes/`, and `controllers/`.
3. The database schema in `db/database.js` will automatically update itself on the next startup if new columns are added.

---

## 🤖 Note for AI Agents

When modifying this codebase, prioritize **performance** and **SEO**. Every new public route must be added to the `injectSEOMeta` function in `server.js` to ensure crawlability. Always use the `useAuthStore` for state management and ensure `AuthGuard` or `Layout` level checks are in place for user-dependent UI.
