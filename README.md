# documenty

A document editor where several people can work on the same document at the same
time. Changes are sent over websockets, so everyone sees edits as they happen.
Written in 2021 as a learning project.

## What it does

- Create, edit and delete documents
- Several people can edit one document at once, with changes shared live
- Register and sign in
- Browse your documents with paging and search

## Stack

| Area | Choice |
| --- | --- |
| Frontend | React, Redux, React Bootstrap |
| Backend | Node.js, Express |
| Database | MongoDB with Mongoose |
| Editor | Quill |
| Realtime | Socket.IO |
| Auth | JSON Web Tokens, bcrypt for hashing |

## Layout

```
client/   React app
server/   Express API and the Socket.IO server
```

## How the live editing works

The Express server also runs Socket.IO. When someone opens a document they join
a room named after the document id. The editor is Quill, so an edit is a small
delta rather than the whole document. That delta is broadcast to the rest of the
room and applied there, which keeps every open editor in step without polling and
without sending the full text on each keystroke.

## Running it locally

```bash
npm install
cd client && npm install && cd ..
```

Create a `.env` file in the project root:

```
NODE_ENV=development
PORT=5000
MONGO_URI=your mongodb connection string
JWT_SECRET=any random string
```

Then start both halves:

```bash
npm run dev
```

## Status

Finished as a learning project and not maintained. It is kept here as a record
of building something realtime with websockets.
