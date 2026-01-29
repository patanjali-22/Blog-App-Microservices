# 📝 Blog App - Microservices Architecture

A full-stack blogging platform built with **microservices architecture**, featuring AI-powered content generation, real-time caching, and modern authentication.

![Next.js](https://img.shields.io/badge/Next.js-15.3-black?style=for-the-badge&logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue?style=for-the-badge&logo=typescript)
![Node.js](https://img.shields.io/badge/Node.js-Express-green?style=for-the-badge&logo=node.js)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Neon-blue?style=for-the-badge&logo=postgresql)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-green?style=for-the-badge&logo=mongodb)
![Redis](https://img.shields.io/badge/Redis-Cache-red?style=for-the-badge&logo=redis)

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                         FRONTEND                                 │
│                    (Next.js + TypeScript)                        │
│                    Deployed on Vercel                            │
└──────────────────────────┬──────────────────────────────────────┘
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│  USER SERVICE   │ │ AUTHOR SERVICE  │ │  BLOG SERVICE   │
│   (Express)     │ │   (Express)     │ │   (Express)     │
│                 │ │                 │ │                 │
│  • Google OAuth │ │  • Create Blog  │ │  • Get Blogs    │
│  • JWT Auth     │ │  • Update Blog  │ │  • Comments     │
│  • Profile Mgmt │ │  • Delete Blog  │ │  • Save Blogs   │
│                 │ │  • AI Features  │ │  • Redis Cache  │
└────────┬────────┘ └────────┬────────┘ └────────┬────────┘
         │                   │                   │
         ▼                   │                   │
┌─────────────────┐          │          ┌───────┴───────┐
│    MongoDB      │          │          │     Redis     │
│    (Users)      │          │          │    (Cache)    │
└─────────────────┘          │          └───────────────┘
                             │
              ┌──────────────┴──────────────┐
              │         RabbitMQ            │
              │   (Cache Invalidation)      │
              └──────────────┬──────────────┘
                             │
                             ▼
              ┌─────────────────────────────┐
              │       PostgreSQL            │
              │   (Blogs, Comments, Saved)  │
              │      Hosted on Neon         │
              └─────────────────────────────┘
```

## ✨ Features

### 🔐 Authentication
- Google OAuth 2.0 integration
- JWT-based authentication
- Secure token management with cookies

### 📝 Blog Management
- Create, Read, Update, Delete blogs
- Rich text editor with Jodit
- Image upload with Cloudinary
- Category-based organization

### 🤖 AI-Powered Features
- **AI Title Correction** - Fix grammar in blog titles using Google Gemini
- **AI Description Generation** - Auto-generate blog descriptions
- **AI Content Grammar Check** - Improve blog content grammar

### ⚡ Performance
- Redis caching for fast blog retrieval
- RabbitMQ for async cache invalidation
- Optimized database queries

### 💾 Save & Bookmark
- Save blogs for later reading
- Personal saved blogs collection

### 💬 Comments
- Comment on blogs
- View all comments on a blog

## 🛠️ Tech Stack

### Frontend
| Technology | Purpose |
|------------|---------|
| Next.js 15 | React Framework with App Router |
| TypeScript | Type Safety |
| Tailwind CSS | Styling |
| shadcn/ui | UI Components |
| Axios | HTTP Client |
| Jodit React | Rich Text Editor |

### Backend Services
| Service | Technologies | Database |
|---------|-------------|----------|
| User Service | Express, TypeScript, Mongoose | MongoDB Atlas |
| Author Service | Express, TypeScript, Neon | PostgreSQL (Neon) |
| Blog Service | Express, TypeScript, Redis | PostgreSQL (Neon) |

### Infrastructure
| Technology | Purpose |
|------------|---------|
| RabbitMQ | Message Queue for Cache Invalidation |
| Redis | Caching Layer |
| Cloudinary | Image Storage & CDN |
| Google Gemini | AI Features |

### Deployment
| Service | Platform |
|---------|----------|
| Frontend | Vercel |
| Backend Services | Render |
| PostgreSQL | Neon |
| MongoDB | MongoDB Atlas |
| Redis | Redis Cloud |
| RabbitMQ | CloudAMQP |

## 📁 Project Structure

```
Blog-App-Microservices/
├── frontend/                    # Next.js Frontend
│   ├── src/
│   │   ├── app/                # App Router Pages
│   │   │   ├── blog/           # Blog CRUD Pages
│   │   │   ├── blogs/          # Blog Listing
│   │   │   ├── login/          # Authentication
│   │   │   └── profile/        # User Profile
│   │   ├── components/         # React Components
│   │   │   ├── ui/             # shadcn/ui Components
│   │   │   ├── navbar.tsx
│   │   │   ├── sidebar.tsx
│   │   │   └── BlogCard.tsx
│   │   ├── context/            # React Context
│   │   ├── hooks/              # Custom Hooks
│   │   └── lib/                # Utilities
│   └── public/                 # Static Assets
│
└── services/
    ├── user/                   # User Microservice
    │   └── src/
    │       ├── controllers/    # Route Handlers
    │       ├── middleware/     # Auth, Multer
    │       ├── model/          # Mongoose Models
    │       ├── routes/         # Express Routes
    │       └── utils/          # Helpers
    │
    ├── author/                 # Author Microservice
    │   └── src/
    │       ├── controllers/    # Blog CRUD + AI
    │       ├── middlewares/    # Auth, Multer
    │       ├── routes/         # Express Routes
    │       └── utils/          # DB, RabbitMQ
    │
    └── blog/                   # Blog Microservice
        └── src/
            ├── controllers/    # Blog Read + Cache
            ├── middleware/     # Auth
            ├── routes/         # Express Routes
            └── utils/          # DB, Redis Consumer
```

## 🚀 Getting Started

### Prerequisites
- Node.js 18+
- npm or yarn
- MongoDB Atlas account
- Neon PostgreSQL account
- Redis Cloud account
- CloudAMQP account
- Cloudinary account
- Google Cloud Console (for OAuth)
- Google AI Studio (for Gemini API)

### Environment Variables

#### User Service (`services/user/.env`)
```env
PORT=5000
MONGO_URL=mongodb+srv://...
JWT_SECRET=your_jwt_secret
Google_Client_ID=your_google_client_id
Google_Client_Secret=your_google_client_secret
Cloud_Name=your_cloudinary_name
Cloud_Api_Key=your_cloudinary_key
Cloud_Api_Secret=your_cloudinary_secret
```

#### Author Service (`services/author/.env`)
```env
PORT=5001
DB_URL=postgresql://...
JWT_SECRET=your_jwt_secret
Cloud_Name=your_cloudinary_name
Cloud_Api_Key=your_cloudinary_key
Cloud_Api_Secret=your_cloudinary_secret
Rabbimq_Host=your_rabbitmq_host
Rabbimq_Username=your_rabbitmq_user
Rabbimq_Password=your_rabbitmq_password
Gemini_Api_Key=your_gemini_api_key
```

#### Blog Service (`services/blog/.env`)
```env
PORT=5002
DB_URL=postgresql://...
JWT_SECRET=your_jwt_secret
Rabbimq_Host=your_rabbitmq_host
Rabbimq_Username=your_rabbitmq_user
Rabbimq_Password=your_rabbitmq_password
Redis_Host=your_redis_host
Redis_Port=your_redis_port
Redis_Password=your_redis_password
```

#### Frontend (`frontend/.env.local`)
```env
NEXT_PUBLIC_USER_SERVICE=http://localhost:5000
NEXT_PUBLIC_AUTHOR_SERVICE=http://localhost:5001
NEXT_PUBLIC_BLOG_SERVICE=http://localhost:5002
```

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/patanjali-22/Blog-App-Microservices.git
cd Blog-App-Microservices
```

2. **Install dependencies for each service**
```bash
# User Service
cd services/user
npm install

# Author Service
cd ../author
npm install

# Blog Service
cd ../blog
npm install

# Frontend
cd ../../frontend
npm install
```

3. **Set up environment variables**
Create `.env` files in each service directory with the required variables.

4. **Run the services**

```bash
# Terminal 1 - User Service
cd services/user
npm run dev

# Terminal 2 - Author Service
cd services/author
npm run dev

# Terminal 3 - Blog Service
cd services/blog
npm run dev

# Terminal 4 - Frontend
cd frontend
npm run dev
```

5. **Access the application**
Open [http://localhost:3000](http://localhost:3000) in your browser.

## 📡 API Endpoints

### User Service (Port 5000)
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/google` | Google OAuth Login |
| GET | `/api/v1/me` | Get Current User |
| GET | `/api/v1/user/:id` | Get User by ID |
| PUT | `/api/v1/user` | Update User Profile |

### Author Service (Port 5001)
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/blog/new` | Create Blog |
| POST | `/api/v1/blog/:id` | Update Blog |
| DELETE | `/api/v1/blog/:id` | Delete Blog |
| POST | `/api/v1/ai/title` | AI Title Correction |
| POST | `/api/v1/ai/descripiton` | AI Description Generation |
| POST | `/api/v1/ai/blog` | AI Blog Grammar Check |

### Blog Service (Port 5002)
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/blog/all` | Get All Blogs (Cached) |
| GET | `/api/v1/blog/:id` | Get Blog by ID |
| GET | `/api/v1/blog/comment/:id` | Get Blog Comments |
| POST | `/api/v1/blog/comment/:id` | Add Comment |
| POST | `/api/v1/blog/save/:id` | Save/Unsave Blog |
| GET | `/api/v1/blog/save/all` | Get Saved Blogs |
| GET | `/api/v1/blog/author/:id` | Get Blogs by Author |

## 🔄 Message Queue Flow

```
Author Service                    RabbitMQ                    Blog Service
     │                               │                             │
     │  Create/Update/Delete Blog    │                             │
     ├──────────────────────────────>│                             │
     │                               │                             │
     │  Publish Cache Invalidation   │                             │
     │  Message to Queue             │                             │
     │                               │  Consume Message            │
     │                               ├────────────────────────────>│
     │                               │                             │
     │                               │  Invalidate Redis Cache     │
     │                               │  (blogs:*, blog:id)         │
     │                               │                             │
```

## 🎨 Screenshots

### Home Page
The landing page with navigation to blogs and login.

### Blogs Page
Grid view of all blogs with category filtering.

### Blog Detail
Full blog view with comments section.

### Create/Edit Blog
Rich text editor with AI-powered features.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License.

## 👨‍💻 Author

**Patanjali U**
- GitHub: [@patanjali-22](https://github.com/patanjali-22)

---

⭐ Star this repo if you found it helpful!
