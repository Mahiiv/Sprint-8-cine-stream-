# Cine-Stream 🎬

A small Netflix-style movie explorer built with React and the TMDB API. You can browse popular movies, search for any movie and save your favorites.

**Live Demo:** https://sprint8cinestream.vercel.app/
---

## Features

- **Popular movies grid** showing the poster, title, release year and rating
- **Search** using the TMDB search endpoint
- **Debounced search**: the app waits until you stop typing for 500ms, so typing "batman" sends 1 request instead of 6
- **Infinite scroll**: when you reach the bottom, the next page loads automatically (using the browser's `IntersectionObserver`)
- **Favorites**: click the heart on any movie to save it. Favorites are stored in `localStorage`, so they stay after you refresh the page
- **Favorites page** at `/favorites`
- **Missing poster handling**: a gray "No Poster" box shows up if a movie has no image, so the grid doesn't break

## Tech Used

- React 18
- Vite
- React Router (for `/` and `/favorites`)
- TMDB API
- Plain CSS
- Deployed on Vercel

## How to Run It Locally

1. Clone the repo and go into the folder

   ```
   git clone YOUR_GITHUB_REPO_LINK
   cd cine-stream
   ```

2. Install the packages

   ```
   npm install
   ```

3. Get a TMDB token
   - Make a free account on [themoviedb.org](https://www.themoviedb.org) and verify your email
   - Go to Settings → API and create a Developer key
   - Copy the long **API Read Access Token** (the one that starts with `eyJ`)

4. Create a file called `.env` in the main folder (next to `package.json`) and add:

   ```
   VITE_TMDB_KEY=your_read_access_token_here
   ```

   No quotes, no spaces. See `.env.example` for the format.

5. Start the app

   ```
   npm run dev
   ```

6. Open the link it shows in the terminal (usually `http://localhost:5173`)

> If you change `.env`, stop the server and run `npm run dev` again. Vite only reads it on startup.

## Deploying to Vercel

1. Push the project to GitHub (do **not** upload `.env`)
2. Import the repo on Vercel
3. Under **Environment Variables**, add `VITE_TMDB_KEY` with your token
4. Deploy. If you add the variable later, redeploy so it gets picked up
5. `vercel.json` is included so refreshing `/favorites` doesn't give a 404

## Project Structure

```
cine-stream/
├── src/
│   ├── main.jsx        # starts the app with the router
│   ├── App.jsx         # navbar, routes, favorites state + localStorage
│   ├── Home.jsx        # popular movies, search, debounce, infinite scroll
│   ├── Favorites.jsx   # the /favorites page
│   ├── MovieCard.jsx   # one movie card with the heart button
│   └── App.css         # all styling
├── index.html
├── package.json
├── vite.config.js
├── vercel.json
└── .env.example
```

## How the Main Parts Work

**Infinite scroll:** an invisible div sits under the grid. An `IntersectionObserver` watches it, and when it comes into view the page number goes up by 1. The new movies are added to the old ones with `[...prev, ...newMovies]` so nothing gets overwritten.

**Favorites:** the full movie object is saved in a favorites array. A `useEffect` copies that array into `localStorage` every time it changes, and the array is loaded from `localStorage` when the app starts.


## Credits

Movie data and images come from [TMDB](https://www.themoviedb.org).
