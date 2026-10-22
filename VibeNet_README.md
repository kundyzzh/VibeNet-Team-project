# VibeNet

A social network built with Flask: user accounts, posts with images, friend requests, and private messaging. Team university project (2024).

---

## Features

- **Accounts** — registration, login, session handling, hashed passwords, editable profile with avatar upload and an "about me" field.
- **Posts** — create, view, edit and delete posts with image attachments.
- **Friends** — send, accept and reject friend requests; view a friends list.
- **Messaging** — direct messages and chat threads between users.

---

## Stack

Flask · SQLAlchemy · SQLite · Jinja2 templates · vanilla JavaScript · Werkzeug password hashing · Gunicorn

---

## Data model

| Model | Purpose |
|---|---|
| `User` | account, credentials, profile fields, avatar path |
| `Article` | a post — title, body, image path, timestamp, author FK |
| `Chat` | chat message with sender and receiver FKs and a conversation id |
| `Message` | direct message between two users |
| `Friendship` | friend relationship and request state |

Relationships are declared on both sides with `back_populates`; the two self-referential links on `User` (sent and received messages) are disambiguated with explicit `foreign_keys`.

---

## Layout

```
app.py          routes: home, about, register, login, logout, profile
flaskapp.py     Flask app instance and configuration
db.py           SQLAlchemy models
posting.py      post routes
friends.py      friend request routes
chats.py        chat routes
messages.py     direct message routes
user_page.py    profile page routes
templates/      Jinja2 templates
static/         CSS and JavaScript
Procfile        gunicorn app:app
```

---

## Running it

```bash
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python app.py
```

Runs at `http://localhost:5000`. The SQLite database is created on first run.

---

## Limitations

Student project, kept as a portfolio piece rather than maintained.

- SQLite with no migrations — schema changes mean recreating the database.
- Uploaded files are written straight to `static/`; no type or size validation.
- No CSRF protection and no rate limiting on the auth routes.
- Secrets are read from config rather than the environment.

---

## Author

Kundyz Zhumazhanova — [github.com/kundyzzh](https://github.com/kundyzzh)
