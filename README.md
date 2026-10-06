# Social Help App

A full-stack psychological help platform. Members of a company community can explore shared content (videos, blogs, events), find peer buddies by interest, and apply to take on greater roles in the community. Administrators review role applications and manage users, companies, and content from a dashboard.

*Implemented in April 2022, by PROPEP+ fast track Group 6 consisting of Spas S.B. Mitsev, Mohammad Baghban Haghighi, Ioannis Kyrousis, Nearchos Katsanikakis, Abraham A.B.S. Ackom-Mensah and Rozalina Miladiniva.*

## Repository layout

| Path | Description |
|---|---|
| `social-help-backend/` | ASP.NET Core 6 Web API (C#) with MongoDB persistence |
| `social-help-frontend/` | React 17 SPA (Create React App) |

## Features

- **Accounts** — register/login with JWT authentication; registration is linked to a company via its invite code
- **Roles** — Member, Buddy, Professional, Administrator, Blocked
- **Role requests** — users apply to become a Buddy or a licensed Professional; admins approve or deny from the dashboard
- **Activities** — three content types (Video, Blog, Event), each with its own required fields, tag support, and company scoping
- **Buddy matching** — buddies are matched against requested preference categories and ranked by overlap and experience
- **Admin dashboard** — role request review, user & company management, role distribution charts

## Backend

- .NET 6, MongoDB.Driver, JWT bearer authentication, Swagger (dev only)
- Layered structure: `Controllers` → services (interfaces in `SocialHelp.Core/Services/Interfaces`, implementations in `Services/Managers`) → Mongo collections via `DbClient`
- Database name and collection names are provided through configuration/environment variables (see `launchSettings.json`: `DATABASE_NAME`, `USERS_COLLECTION_NAME`, …)
- A MongoDB instance is required; `Connection_String` must be supplied through user secrets or environment variables

Run:

```
cd social-help-backend
dotnet run --project SocialHelp     # serves on http://localhost:5012, Swagger at /swagger
```

## Frontend

- React 17, React Bootstrap + cdbreact, DevExtreme admin widgets, Chart.js, Axios
- API base URL defaults to `http://localhost:5012/` (see `src/App.js`); the JWT token is kept in `localStorage` and attached to requests by an interceptor

Run:

```
cd social-help-frontend
npm install
npm start     # dev server on https://localhost:3000 (HTTPS=TRUE in .env)
```