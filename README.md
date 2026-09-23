# GitTogether

A full-stack project collaboration platform built as a Georgia Tech WebDev team project. This repository is [Dylan Soutter's fork](https://github.com/dylansoutter/DylanSoutterGitTogether) of the [team repository](https://github.com/JWiriadinata/GitTogether).

**Tech:** React · TypeScript · Vite · Node.js · Express · MongoDB · Mongoose · JWT

## My contributions

- Implemented backend registration and login with password hashing and JWT issuance.
- Added the Express authentication routes and connected them to the server.
- Built the Mongoose `Project` model, including the creator reference, technology and role fields, open status, and timestamps.
- Refined the authentication controller and helped check API behavior with Postman.

Other team members implemented the user profile API, project controllers, owner authorization, and frontend. The fork and its commit history preserve that shared credit.

## Architecture

```text
React / Vite frontend
       │ HTTP /api
       ▼
Express routes and controllers
       ├── POST /api/auth/register, POST /api/auth/login
       │       └── bcrypt password hash + signed JWT
       ├── GET /api/users/me, PATCH /api/users/me  [JWT required]
       └── POST /api/projects                      [JWT required]
           GET /api/projects, GET /api/projects/:id
           PATCH /api/projects/:id                 [creator only]
           DELETE /api/projects/:id                [creator only]
       │
       ▼
Mongoose User and Project models → MongoDB
```

The active frontend has registration and login form wiring, but its home, project list, project creation dialog, and profile screens currently use sample data or local-only interactions. The API routes exist in the backend, but the full browser workflow is not integrated. The UI still displays the prototype name **ProjectHub**.

## Screenshots

These are screenshots of the current local **frontend prototype**. Project counts, listings, and profile details are sample data; the creation dialog does not save a project.

| Login | Project browser | Create project dialog |
| --- | --- | --- |
| ![Login screen](portfolio-assets/login-preview.png) | ![Project browser with sample listings](portfolio-assets/projects-preview.png) | ![Project creation dialog](portfolio-assets/create-project-preview.png) |

[More preview assets, including the profile screen and a short UI walkthrough](portfolio-assets/README.md)

## Local setup

You need Node.js, npm, and a reachable MongoDB instance. Keep real connection strings and JWT secrets in the ignored backend `.env` file; never commit them or show them in screenshots.

1. In `my-app/backend`, run `npm ci`, then copy `.env.example` to `.env`. Set `MONGO_URI` to your own local or hosted MongoDB connection, set a unique `JWT_SECRET`, and set `PORT=5001` to match the frontend's Vite proxy.
2. Run `npm start` from `my-app/backend`.
3. In a separate terminal, run `npm ci` and then `npm run dev` from `my-app/frontend`.
4. Open `http://localhost:3000` for the UI. The backend responds at `http://localhost:5001/`.

The frontend currently builds with `npx vite build`. Its `npm run build` script runs `tsc` first and fails because the repository has no `tsconfig.json`; this is one reason the project is not presented as a live deployment.

## Contributors

GitTogether was built by a Georgia Tech WebDev team. See the [upstream repository](https://github.com/JWiriadinata/GitTogether), [fork history](https://github.com/dylansoutter/DylanSoutterGitTogether/commits/main/), and individual commits for attribution. My focus was backend authentication and the Project model.
