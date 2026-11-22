# Secure Notes Frontend

A plain HTML/CSS/JavaScript frontend (no framework, no template, no build step) for the
[Secure Notes API](../secure-notes-api). Everything lives in one file: `index.html`.

## Run

1. Point the page at your API. At the top of the script in `index.html`:

   ```js
   const API = "http://localhost:6001/api/v1";
   ```

2. Allow this page's origin in the backend `.env`, then restart the backend (without it the browser blocks requests with a CORS error):

   ```
   CLIENT_URLS=http://localhost:5173
   ```

3. Serve the folder (opening the file directly with `file://` will not work):

   ```bash
   npx serve -l 5173 .
   # or
   python3 -m http.server 5173
   ```

4. Open http://localhost:5173

The origin in `CLIENT_URLS` must match the address in the browser exactly (`localhost` and `127.0.0.1` are different origins).

## What it covers (all 22 API endpoints)

| Area | Screen |
|---|---|
| Register, login, logout | first page |
| Notes: create, list (own, or all for admin), open one, edit, delete, filter by owner (admin) | Notes tab |
| Posts: create, list, open one, edit, delete, posts of one user (`$lookup`) | Posts tab |
| Users (admin): create, list, open one, edit, delete | Users tab |
| Users grouped by interest (admin, aggregation) | Interests tab |
| Update profile, change password | Profile tab |

Lists use cursor pagination: "Load more" sends `?cursor=<meta.nextCursor>` from the previous page.
