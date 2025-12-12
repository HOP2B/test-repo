# AI Chat App

A Next.js application that allows users to select AI characters and chat with them using Groq's ultra-fast LLM API. Supports multiple languages including Mongolian and English.

## Features

- **Character Selection**: Beautiful grid layout to choose from multiple AI characters
- **Real-time AI Chat**: Fast responses powered by Groq (Llama 3.3 70B)
- **Multilingual Support**: Understands and responds in Mongolian and English
- **Message History**: All conversations are saved to PostgreSQL database
- **Character Management**: Admin panel to create and manage AI characters
- **Image Upload**: Upload character avatars using Vercel Blob Storage

## Tech Stack

- **Framework**: Next.js 16 with App Router
- **Database**: PostgreSQL with Prisma ORM
- **AI Provider**: Groq API (Llama 3.3 70B Versatile)
- **Storage**: Vercel Blob for image uploads
- **Styling**: Tailwind CSS
- **UI Components**: Radix UI

## Getting Started

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd ai-chat-app
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Set Up Environment Variables

Copy the example environment file:

```bash
cp .env.example .env
```

Then edit `.env` and add your API keys:

#### Required

- **DATABASE_URL**: PostgreSQL connection string
  - Get from [Neon](https://neon.tech) (free) or your preferred provider

- **GROQ_API_KEY**: Groq API key for AI chat
  - Sign up at [Groq Console](https://console.groq.com)
  - Go to [API Keys](https://console.groq.com/keys)
  - Create a new key (free tier: 1,000 requests/day)

- **BLOB_READ_WRITE_TOKEN**: Vercel Blob storage token
  - Create at [Vercel Dashboard](https://vercel.com/dashboard/stores)

### 4. Set Up Database

Run Prisma migrations to create database tables:

```bash
npx prisma generate
npx prisma db push
```

### 5. Run the Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see your app.

## Usage

### Create Characters (Admin)

1. Go to [http://localhost:3000/admin/characters](http://localhost:3000/admin/characters)
2. Click "Create Character"
3. Fill in character details:
   - **Name**: Character's name
   - **Description**: Brief description of the character
   - **Base Prompt**: System prompt that defines character personality
   - **Greeting Text**: First message from the character
   - **Image**: Upload character avatar
4. Click "Create"

### Chat with Characters

1. Go to [http://localhost:3000](http://localhost:3000)
2. Select a character from the grid
3. Start chatting!
4. The AI will respond in the same language you use (Mongolian or English)

## Project Structure

```text
ai-chat-app/
├── app/
│   ├── page.tsx                    # Character selection page
│   ├── chat/[characterId]/         # Chat page for each character
│   ├── admin/characters/           # Character management admin panel
│   └── api/
│       ├── character/              # Character CRUD endpoints
│       │   └── [characterId]/
│       │       └── message/        # Chat message endpoint
│       └── upload/                 # Image upload endpoint
├── prisma/
│   └── schema.prisma               # Database schema
├── components/ui/                   # Reusable UI components
├── lib/                            # Utility functions
└── public/                         # Static assets
```

## Available AI Models

The app uses Groq with the following model:

- **llama-3.3-70b-versatile** (default)
  - 300+ tokens/second
  - Excellent multilingual support
  - 1,000 free requests/day

You can change the model in `app/api/character/[characterId]/message/route.ts` (line 73) to:

- `llama-3.1-70b-versatile`
- `mixtral-8x7b-32768`
- `gemma2-9b-it`

## API Endpoints

- `GET /api/character` - List all characters
- `POST /api/character` - Create new character
- `GET /api/character/[id]` - Get character details
- `PUT /api/character/[id]` - Update character
- `DELETE /api/character/[id]` - Delete character
- `GET /api/character/[id]/message` - Get chat history
- `POST /api/character/[id]/message` - Send message and get AI response
- `POST /api/upload` - Upload images

## Database Schema

### Character

- `id`: Unique identifier
- `name`: Character name
- `description`: Character description
- `image`: Avatar URL
- `basePrompt`: System prompt for AI
- `greetingText`: Initial greeting message

### Message

- `id`: Unique identifier
- `content`: Message text
- `role`: "user" or "model"
- `characterId`: Reference to character
- `createdAt`: Timestamp

## Deployment

### Deploy to Vercel

1. Push your code to GitHub
2. Import your repository on [Vercel](https://vercel.com)
3. Add environment variables in Vercel dashboard
4. Deploy!

### Environment Variables on Vercel

Make sure to add all variables from `.env.example` to your Vercel project settings.

## Learn More

- [Next.js Documentation](https://nextjs.org/docs)
- [Groq Documentation](https://console.groq.com/docs)
- [Prisma Documentation](https://www.prisma.io/docs)
- [Vercel Blob Documentation](https://vercel.com/docs/storage/vercel-blob)

## License

MIT

## Support

For issues and questions, please open an issue on GitHub.
