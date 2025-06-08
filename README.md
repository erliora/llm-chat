# LLM Chat - Multi-Model AI Chat Application

An open-source chat application that allows you to interact with multiple Large Language Models (LLMs) in one unified interface. Built with Remix, TypeScript, Tailwind CSS, and Supabase.

## 🚀 Features

- **Multi-Model Support**: Chat with OpenAI GPT, Anthropic Claude, Google Gemini, Hugging Face models, and more
- **Real-time Streaming**: See AI responses as they're generated with resumable streams
- **File Attachments**: Upload and share images, PDFs, and text files (up to 10MB)
- **Syntax Highlighting**: Automatic code block detection and highlighting with Prism.js
- **Chat Branching**: Fork conversations to explore different paths
- **Image Generation**: AI-powered image creation with Stable Diffusion and DALL·E
- **Web Search Integration**: Real-time web search via Linkup API
- **Responsive Design**: Works seamlessly on desktop and mobile devices
- **Open Source**: MIT licensed for community contributions

## 🛠️ Tech Stack

- **Frontend**: Remix (React Router v7), TypeScript, Tailwind CSS
- **Backend**: Remix server-side functions, Node.js
- **Database**: Supabase (PostgreSQL with real-time sync)
- **Authentication**: Supabase Auth with OAuth support
- **LLM Providers**: OpenAI, Anthropic, Google Gemini, Hugging Face
- **Image Generation**: Stable Diffusion, OpenAI DALL·E
- **Search**: Linkup API
- **Deployment**: Vercel, Netlify, or any Node.js hosting

## 📋 Prerequisites

- Node.js 18+ 
- Yarn 1.22.19+
- Supabase account
- API keys for desired LLM providers

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd llm-chat
```

### 2. Install Dependencies

```bash
cd frontend
npm install
```

### 3. Environment Setup

Create a `.env` file in the project root:

```env
# Supabase Configuration
SUPABASE_URL=your_supabase_project_url
SUPABASE_ANON_KEY=your_supabase_anon_key

# JWT Secret for session management
JWT_SECRET=your_jwt_secret_key

# LLM Provider API Keys (add the ones you want to use)
OPENAI_API_KEY=your_openai_api_key
ANTHROPIC_API_KEY=your_anthropic_api_key
GOOGLE_GEMINI_API_KEY=your_google_gemini_api_key
HUGGINGFACE_API_KEY=your_huggingface_api_key

# Web Search
LINKUP_API_KEY=your_linkup_api_key
```

### 4. Database Setup

1. Create a new Supabase project at [supabase.com](https://supabase.com)
2. Run the following SQL in your Supabase SQL editor:

```sql
-- Create users table
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email TEXT UNIQUE NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Create chats table
CREATE TABLE chats (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  title TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Create messages table
CREATE TABLE messages (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  chat_id UUID REFERENCES chats(id) ON DELETE CASCADE,
  parent_message_id UUID REFERENCES messages(id),
  role TEXT CHECK (role IN ('user', 'assistant', 'system')),
  content TEXT NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Create indexes for better performance
CREATE INDEX idx_chats_user_id ON chats(user_id);
CREATE INDEX idx_messages_chat_id ON messages(chat_id);
CREATE INDEX idx_messages_created_at ON messages(created_at);
```

### 5. Start Development Server

```bash
npm run dev
```

The application will be available at `http://localhost:3000`

## 🎯 Usage

1. **Start a Chat**: Click "Start Chatting" on the homepage
2. **Select a Model**: Choose your preferred AI model from the dropdown
3. **Send Messages**: Type your message and press Enter or click Send
4. **Upload Files**: Drag and drop or click to upload images, PDFs, or text files
5. **Generate Images**: Use the image generation feature for AI-created visuals
6. **Branch Conversations**: Fork any message to explore different conversation paths
7. **Share Chats**: Generate read-only links to share conversations

## 🔧 Configuration

### Adding New LLM Providers

1. Add your provider to `app/lib/llm-providers.server.ts`
2. Implement the `LLMProvider` interface
3. Add the provider to the `providers` registry
4. Update the environment variables

### Customizing the UI

- Modify Tailwind classes in components
- Update the color scheme in `tailwind.config.ts`
- Add new components in `app/components/`

## 🚀 Deployment

### Vercel (Recommended)

1. Connect your GitHub repository to Vercel
2. Add environment variables in Vercel dashboard
3. Deploy automatically on push to main branch

### Netlify

1. Build the project: `npm run build`
2. Deploy the `build` folder to Netlify
3. Configure environment variables

### Self-Hosting

1. Build the project: `npm run build`
2. Start the server: `npm start`
3. Configure reverse proxy (nginx/Apache)

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- 📖 [Documentation](docs/)
- 🐛 [Issue Tracker](issues/)
- 💬 [Discussions](discussions/)
- 📧 Email: support@llmchat.dev

## 🙏 Acknowledgments

- [Remix](https://remix.run/) for the amazing full-stack framework
- [Supabase](https://supabase.com/) for the backend infrastructure
- [Tailwind CSS](https://tailwindcss.com/) for the styling system
- All the LLM providers for making AI accessible
- The open-source community for inspiration and contributions

---

**Built with ❤️ by the LLM Chat community** 