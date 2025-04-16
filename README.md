# Expense Tracker for Vercel

A full-stack expense tracker application with receipt management capabilities, optimized for Vercel deployment. This application allows users to track expenses, manage receipts, and organize expenses by trips.

## Features

- **User Authentication**: Secure login and registration system
- **Expense Management**: Create, read, update, and delete expenses
- **Receipt Management**: Upload, view, and manage receipts for expenses
  - **OCR Support**: Extract data from receipts using AI (Google Gemini, OpenAI, Anthropic, or OpenRouter)
- **Trip Organization**: Organize expenses by trips
- **Data Visualization**: View expense trends and summaries
- **Responsive UI**: Modern UI built with React and Tailwind CSS
- **Vercel Optimized**: Configured for seamless deployment on Vercel
- **Supabase Integration**: PostgreSQL database and storage for receipts

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
- PostgreSQL (via Supabase)
- Drizzle ORM
- Supabase Storage (File storage)

## Getting Started

### Prerequisites
- Node.js (v16+)
- npm or yarn
- Supabase account
- Vercel account

### Installation

1. Clone the repository
```bash
git clone https://github.com/yourusername/expenseTracker_Vercel.git
cd expenseTracker_Vercel
```

2. Install dependencies
```bash
npm install
```

3. Create a `.env.local` file in the root directory based on the `.env.example` file:
```bash
cp .env.example .env.local
```

4. Update the `.env.local` file with your own values:
```
DATABASE_URL=your_supabase_database_connection_string
SUPABASE_URL=your_supabase_url
SUPABASE_SERVICE_KEY=your_supabase_service_key
SESSION_SECRET=your_session_secret
# Optional OCR API keys
GEMINI_API_KEY=your_gemini_api_key
OPENAI_API_KEY=your_openai_api_key
ANTHROPIC_API_KEY=your_anthropic_api_key
OPENROUTER_API_KEY=your_openrouter_api_key
```

5. Run the database migrations
```bash
npm run migrate
```

6. Run the development server
```bash
npm run dev
```

7. Open [http://localhost:3000](http://localhost:3000) in your browser

## Development Setup

### Database Setup

This project uses Supabase PostgreSQL for the database. To set up the database:

1. Create a Supabase project
2. Get your database connection string from the Supabase dashboard
3. Update the `DATABASE_URL` in your `.env.local` file
4. Run the migrations with `npm run migrate`

### Storage Setup

This project uses Supabase Storage for storing receipt files:

1. Create a storage bucket named `expense-receipts` in your Supabase project
2. Set the appropriate permissions for the bucket
3. Get your Supabase service key from the Supabase dashboard
4. Update the `SUPABASE_SERVICE_KEY` in your `.env.local` file

### OCR Setup (Optional)

For receipt OCR functionality, you can configure one or more of the following AI services:

- Google Gemini
- OpenAI
- Anthropic Claude
- OpenRouter

Add the corresponding API keys to your `.env.local` file.

## Deployment

For detailed deployment instructions, please refer to the [DEPLOYMENT.md](./DEPLOYMENT.md) file.

In summary, to deploy to Vercel:

1. Push your code to GitHub
2. Import the repository in Vercel
3. Configure the environment variables in Vercel
4. Deploy

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

MIT