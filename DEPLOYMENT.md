# Deployment Guide for ExpenseTracker Vercel

This guide provides step-by-step instructions for deploying the ExpenseTracker application to Vercel with Supabase as the database and storage provider.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Setting Up Supabase](#setting-up-supabase)
3. [Configuring Environment Variables](#configuring-environment-variables)
4. [Deploying to Vercel](#deploying-to-vercel)
5. [Verifying the Deployment](#verifying-the-deployment)
6. [Troubleshooting](#troubleshooting)

## Prerequisites

Before you begin, ensure you have the following:
- A [Vercel](https://vercel.com) account
- A [Supabase](https://supabase.com) account
- [Node.js](https://nodejs.org) (v16 or higher) installed
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/) installed
- [Git](https://git-scm.com/) installed

## Setting Up Supabase

### 1. Create a Supabase Project

1. Log in to the [Supabase Dashboard](https://app.supabase.com/)
2. Click "New Project"
3. Enter a name for your project
4. Set a secure database password
5. Choose a region closest to your users
6. Click "Create new project"

### 2. Set Up the Database

1. Once your project is created, go to the SQL Editor
2. Run the initial migration script to create the necessary tables:
   - You can find the migration scripts in the `migrations` folder of the project
   - Copy and paste the SQL from these files into the SQL Editor
   - Execute the SQL to create the tables

### 3. Create a Storage Bucket for Receipts

1. In the Supabase dashboard, navigate to "Storage"
2. Click "Create new bucket"
3. Name the bucket `expense-receipts`
4. Set the bucket to private (uncheck "Public bucket")
5. Click "Create bucket"

### 4. Configure Storage Permissions

1. Go to "Storage" > "Policies"
2. For the `expense-receipts` bucket, add the following policies:

   **For authenticated users to upload files:**
   - Click "Add Policy"
   - Select "Create custom policy"
   - Name: "Allow authenticated uploads"
   - Policy definition:
     ```sql
     (auth.uid() = owner) AND (bucket_id = 'expense-receipts')
     ```
   - Click "Save policy"

   **For authenticated users to read their own files:**
   - Click "Add Policy"
   - Select "Create custom policy"
   - Name: "Allow authenticated downloads"
   - Policy definition:
     ```sql
     (auth.uid() = owner) AND (bucket_id = 'expense-receipts')
     ```
   - Click "Save policy"

### 5. Generate a Service Role Key

1. In the Supabase dashboard, go to "Project Settings" > "API"
2. Under "Project API keys", find the "service_role" key
3. Copy this key and save it securely (you'll need it for the environment variables)

## Configuring Environment Variables

### 1. Prepare Your Environment Variables

Create a `.env.local` file in your local development environment with the following variables:

```
DATABASE_URL=postgresql://postgres:[password]@[project-id].supabase.co:6543/postgres
SUPABASE_URL=https://[project-id].supabase.co
SUPABASE_SERVICE_KEY=your-supabase-service-key
SESSION_SECRET=your-session-secret-key
GEMINI_API_KEY=your-gemini-api-key (optional)
OPENAI_API_KEY=your-openai-api-key (optional)
ANTHROPIC_API_KEY=your-anthropic-api-key (optional)
OPENROUTER_API_KEY=your-openrouter-api-key (optional)
```

Replace the placeholders with your actual values:
- `[password]`: Your Supabase database password
- `[project-id]`: Your Supabase project ID
- `your-supabase-service-key`: The service role key you copied earlier
- `your-session-secret-key`: A strong random string for session encryption
- OCR API keys: Add these if you want to use OCR features

### 2. Set Up Environment Variables in Vercel

1. Log in to your [Vercel Dashboard](https://vercel.com/dashboard)
2. Select your project (or import it if you haven't already)
3. Go to "Settings" > "Environment Variables"
4. Add each of the environment variables from your `.env.local` file
5. Make sure to set them for Production, Preview, and Development environments as needed
6. Click "Save" to apply the changes

## Deploying to Vercel

### 1. Install Vercel CLI (Optional)

If you prefer using the command line:

```bash
npm install -g vercel
vercel login
```

### 2. Deploy Your Project

#### Option 1: Using Vercel Dashboard (Recommended for first deployment)

1. Go to the [Vercel Dashboard](https://vercel.com/dashboard)
2. Click "Add New" > "Project"
3. Import your Git repository
4. Configure the project settings:
   - Framework Preset: Other
   - Build Command: `npm run vercel-build`
   - Output Directory: `dist/public`
5. Click "Deploy"

#### Option 2: Using Vercel CLI

From your project directory:

```bash
vercel
```

Follow the prompts to configure your project, then:

```bash
vercel --prod
```

### 3. Connect to Your Git Repository

For continuous deployment:

1. In the Vercel Dashboard, go to your project
2. Navigate to "Settings" > "Git"
3. Connect to your Git provider if not already connected
4. Select the repository and branch to deploy from
5. Configure the build settings if needed
6. Enable automatic deployments

## Verifying the Deployment

After deployment, verify that everything is working correctly:

1. **User Authentication**: Test registration and login functionality
2. **Database Operations**: Verify CRUD operations for expenses and trips
3. **File Uploads**: Test receipt upload and retrieval
4. **OCR Functionality**: Test OCR with different receipt formats (if configured)
5. **Security Headers**: Verify security headers are properly set
6. **Performance**: Check load times and responsiveness

## Troubleshooting

### Common Issues and Solutions

#### Database Connection Issues

**Problem**: Unable to connect to the database
**Solution**:
- Verify that the `DATABASE_URL` is correct
- Check if the database password is correct
- Ensure that the IP address of your Vercel deployment is allowed in Supabase

#### Storage Access Issues

**Problem**: Unable to upload or retrieve files
**Solution**:
- Verify that the `SUPABASE_SERVICE_KEY` is correct
- Check if the storage bucket exists and has the correct name
- Ensure that the storage policies are properly configured

#### Cold Start Performance Issues

**Problem**: Slow initial response times
**Solution**:
- Consider implementing warming strategies
- Optimize database queries
- Use Edge Functions for critical paths

#### Session Management Issues

**Problem**: Users are logged out unexpectedly
**Solution**:
- Check the `SESSION_SECRET` configuration
- Verify cookie settings in the session configuration
- Ensure that the session store is properly configured

#### Environment Variable Issues

**Problem**: Environment variables not being recognized
**Solution**:
- Verify that all environment variables are set in Vercel
- Check for typos in variable names
- Redeploy after updating environment variables

### Getting Help

If you encounter issues not covered in this guide:
- Check the [Vercel Documentation](https://vercel.com/docs)
- Check the [Supabase Documentation](https://supabase.com/docs)
- Open an issue in the project repository
- Contact the project maintainers