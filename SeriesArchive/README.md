# SeriesArchive

**Anime Discovery and Watchlist Tracking Web Application**

A full-stack web app for browsing anime and keeping a watchlist. Anime data comes from the Jikan API (MyAnimeList), watchlist entries and user accounts are stored in a SQLite database, and anime details are cached locally so pages still load when the external API is unavailable.

> Author: Filip Krpes.

## Features

- Browse popular, currently airing and upcoming anime
- Search anime by title
- Anime detail page with synopsis, score, rank, popularity, season, rating and an embedded trailer
- Registration and login with JWT authentication
- Add anime to the watchlist and track status: Planning, Watching, Completed
- Change watchlist status or remove entries from the profile page
- Local anime cache as a fallback when the Jikan API fails
- Admin panel: list users and delete accounts (admin role only)

## Tech stack

| Area | Technology |
|---|---|
| Frontend | React, React Router, styled-components |
| HTTP client | Axios, Fetch API |
| Backend | Node.js, Express |
| Database | SQLite (sqlite3) |
| External data | Jikan API v4 (MyAnimeList) |
| Security | JWT, bcrypt |

## Architecture

```
Browser (React)
     │
     ├──── Jikan API          (anime lists, search, details, trailers)
     │
     │  REST + JWT
     ▼
Express backend ──── SQLite   (users, watchlist, anime cache)
```

## Project structure

```
SeriesArchive/
├── SeriesArchive-Backend-main/
│   ├── server.js        Express API (auth, watchlist, cache, admin)
│   ├── table.js         Creates the database tables
│   └── addTest.js       Seeds an admin account
└── SeriesArchive-Frontend-main/
    └── src/
        ├── Components/  Homepage, AnimeItem, Profile, AdminPanel, LoginModal, ...
        └── context/     Global state and Jikan API calls
```

## Getting started

### Backend

```bash
cd SeriesArchive-Backend-main/SeriesArchive-Backend-main
npm install
node table.js      # create tables
node addTest.js    # optional: create an admin account
npm start          # runs on http://localhost:3001
```

### Frontend

```bash
cd SeriesArchive-Frontend-main/SeriesArchive-Frontend-main
npm install
npm start          # runs on http://localhost:3000
```

## API

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/register` | Create a user |
| POST | `/api/login` | Log in and receive a JWT |
| GET | `/api/anime` | Get watchlist entries |
| POST | `/api/anime` | Add an anime to the watchlist |
| PUT | `/api/anime/:id` | Update watchlist status |
| DELETE | `/api/anime/:id` | Remove a watchlist entry |
| POST | `/api/anime/cache` | Cache anime details |
| GET | `/api/anime/cache/:mal_id` | Get cached anime details |
| GET | `/api/admin/users` | List users (admin) |
| DELETE | `/api/admin/users/:id` | Delete a user (admin) |
