# Expense Tracker for Vercel

A full-stack expense tracker application with receipt management capabilities, optimized for Vercel deployment. This application allows users to track expenses, manage receipts, and organize expenses by trips.

## Features

- **User Authentication**: Secure login and registration system
- **Expense Management**: Create, read, update, and delete expenses
- **Receipt Management**: Upload, view, and manage receipts for expenses
- **Trip Organization**: Organize expenses by trips
- **Responsive UI**: Modern UI built with React and Tailwind CSS
- **Vercel Optimized**: Configured for seamless deployment on Vercel

## Tech Stack

### Frontend
- React
- TanStack Query (React Query)
- Tailwind CSS
- Shadcn UI Components
- Wouter (Routing)
- Recharts (Charts)
- React Hook Form + Zod (Form validation)

### Backend
- Node.js
- Express
- PostgreSQL (via Neon Database)
- Drizzle ORM
- Vercel Blob Storage (File storage)

## Getting Started

### Prerequisites
- Node.js (v16+)
- npm or yarn
- Neon Database account
- Vercel account

### Installation

1. Clone the repository
```bash
git clone https://github.com/oghenetejiriorukpegmail/expenseTracker_Vercel.git
cd expenseTracker_Vercel
```

2. Install dependencies
```bash
npm install
```

3. Create a `.env.local` file in the root directory with the following variables:
```
DATABASE_URL=your_neon_database_connection_string
BLOB_READ_WRITE_TOKEN=your_vercel_blob_token
SESSION_SECRET=your_session_secret
```

4. Run the development server
```bash
npm run dev
```

### Deploying to Vercel

1. Push your code to GitHub
2. Import the repository in Vercel
3. Configure the environment variables
4. Deploy

## Project Structure

- `client/`: Frontend React application
- `server/`: Backend Express API
- `shared/`: Shared code between frontend and backend
- `api/`: API routes for serverless deployment
- `migrations/`: Database migration files

## License

MIT