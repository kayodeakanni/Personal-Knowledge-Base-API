Personal Knowledge Base / Notes API 🧠

A Node.js + Express + MongoDB backend for a "Second Brain" / Notion-style note-taking app. Full CRUD + advanced filtering, pagination, and search.

**Group 1** | Submission deadline: 18th June 2026 | Presentation: 21st June 2026

Live Demo
**API URL**: `https://pkb-render-app.onrender.com`


---

1. Project Overview
Build a backend API that lets users create, organize, and retrieve personal notes with advanced querying. Designed to mimic core Notion functionality for personal knowledge management.

2. Tech Stack
| Layer | Technology |
| --- | --- |
| Runtime | Node.js + Express |
| Database | MongoDB Atlas + Mongoose ODM |
| Config | dotenv |
| Validation | Joi / Mongoose schema validation |
| Hosting | Render.com Web Service |

3. Data Model: Note
```js
{
  title: String, // required, indexed for text search
  content: String, // required, indexed for text search
  category: String, // optional, e.g. "Work", "Personal"
  tags: [String], // optional
  createdAt: Date, // auto
  updatedAt: Date // auto
}
Text index created on `title` + `content` for fast search.

4. API Endpoints

Core CRUD
Method	Endpoint	Description
POST	`/api/notes`	Create a new note
GET	`/api/notes`	Get all notes with pagination, sorting, search
GET	`/api/notes/:id`	Get single note by ID
PUT	`/api/notes/:id`	Update note by ID
DELETE	`/api/notes/:id`	Delete note by ID
Advanced Query Features on `GET /api/notes`
*Pagination*
`?page=1&limit=10` → page 1, 10 notes per page

*Sorting*
`?sort=createdAt` → oldest first
`?sort=-createdAt` → newest first
`?sort=title` → A-Z by title

*Search & Filtering*
`?search=meeting` or `?q=meeting` → matches title or content
`?category=Work` → filter by category

*Example requests:*
Page 2, 5 notes per page, newest first
GET /api/notes?page=2&limit=5&sort=-createdAt

Search for "API" in title/content, filter by Work category
GET /api/notes?search=API&category=Work

Sort alphabetically by title
GET /api/notes?sort=title&limit=20
5. Setup & Installation

*1. Clone & Install*
git clone <your-repo-url>
cd notes-api
npm install
*2. Environment Variables*
Create `.env` in root:
PORT=5000
MONGO_URI=mongodb+srv://<username>:<password>@cluster0.mongodb.net/notesdb
NODE_ENV=development
*3. Run Locally*
npm run dev
Server runs on `http://localhost:5000`

6. Error Handling
API returns standard HTTP status codes with JSON error messages:
- `200` OK
- `201` Created
- `400` Bad Request - validation failed
- `404` Not Found - note ID doesn’t exist
- `500` Server Error

Example error response:
{
  "success": false,
  "message": "Note not found"
}
7. Project Structure
├── config/ # DB connection
├── controllers/ # Route logic
├── models/ # Mongoose schemas
├── routes/ # Express routes
├── middleware/ # Validation, error handling
├──.env # Environment variables - not committed
├──.gitignore
├── server.js # Entry point
└── README.md

---

Built with ❤️ by Group 1. Questions? Open an issue.
