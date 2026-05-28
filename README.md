# Skill Sync Academy 🚀

A comprehensive web application for managing coding courses, student enrollment, and digital skills training in South Africa.

## 🎯 Project Overview

**Skill Sync Academy** is a full-stack web application built with:
- **Next.js 14** (Frontend + Backend API)
- **PostgreSQL** (Database)
- **Prisma** (ORM)
- **NextAuth.js** (Authentication)
- **Tailwind CSS** (Styling)

## ✨ Features

### Student Features
- ✅ User registration & login
- ✅ Browse available courses
- ✅ Enroll in courses
- ✅ Track learning progress
- ✅ Access course materials
- ✅ Submit assignments
- ✅ View certificates
- ✅ Personal dashboard

### Admin Features
- ✅ Create & manage courses
- ✅ View all students
- ✅ Manage student enrollments
- ✅ View analytics dashboard
- ✅ Send notifications
- ✅ Manage payments

## 🛠 Tech Stack

| Component | Technology |
|-----------|------------|
| **Frontend** | Next.js 14, React 18, Tailwind CSS |
| **Backend** | Next.js API Routes |
| **Database** | PostgreSQL |
| **ORM** | Prisma |
| **Auth** | NextAuth.js + JWT |
| **UI Icons** | Heroicons |
| **Validation** | Zod |
| **Password Hashing** | bcryptjs |

## 🚀 Quick Start

### Prerequisites
```bash
- Node.js 18+
- PostgreSQL 12+
- Git
```

### Installation

```bash
# 1. Clone repository
git clone https://github.com/Dzunani95/skill-sync-academy.git
cd skill-sync-academy

# 2. Install dependencies
npm install

# 3. Setup environment variables
cp .env.example .env.local

# Edit .env.local and add:
# DATABASE_URL="postgresql://user:password@localhost:5432/skill_sync"
# NEXTAUTH_SECRET="your-secret-key-here"
# NEXTAUTH_URL="http://localhost:3000"

# 4. Setup database
npx prisma migrate dev --name init
npx prisma db seed

# 5. Run development server
npm run dev
```

Visit: **http://localhost:3000**

## 📊 API Endpoints

### Authentication
```
POST   /api/auth/signup              - Register new student
POST   /api/auth/login               - Login user
POST   /api/auth/logout              - Logout user
POST   /api/auth/forgot-password     - Request password reset
```

### Student Management (Admin Only)
```
GET    /api/students                 - List all students
GET    /api/students/:id             - Get student details
PUT    /api/students/:id             - Update student
DELETE /api/students/:id             - Delete student
PATCH  /api/students/:id/status      - Change student status
```

### Courses
```
GET    /api/courses                  - Get all courses
POST   /api/courses                  - Create course (Admin)
GET    /api/courses/:id              - Get course details
PUT    /api/courses/:id              - Update course (Admin)
DELETE /api/courses/:id              - Delete course (Admin)
```

### Enrollments
```
POST   /api/enrollments              - Enroll in course
GET    /api/enrollments              - Get user enrollments
DELETE /api/enrollments/:id          - Drop course
```

## 📁 Project Structure

```
skill-sync-academy/
├── app/
│   ├── api/                    # API routes
│   │   ├── auth/               # Authentication endpoints
│   │   │   ├── signup/route.ts
│   │   │   └── login/route.ts
│   │   ├── students/           # Student management
│   │   │   └── route.ts
│   │   └── courses/            # Course management
│   │       └── route.ts
│   ├── auth/                   # Authentication pages
│   │   ├── signup/page.tsx
│   │   └── login/page.tsx
│   ├── dashboard/              # Student dashboard
│   │   └── page.tsx
│   ├── admin/                  # Admin pages
│   │   └── dashboard/page.tsx
│   ├── layout.tsx              # Root layout
│   ├── page.tsx                # Home page
│   └── globals.css             # Global styles
├── components/                 # Reusable React components
│   ├── ui/
│   ├── forms/
│   └── layout/
├── lib/                        # Utility functions
│   ├── auth.ts
│   ├── db.ts
│   └── validations.ts
├── prisma/
│   ├── schema.prisma           # Database schema
│   └── seed.ts                 # Database seeding
├── public/                     # Static assets
├── .env.example                # Environment template
├── .gitignore
├── next.config.js
├── tailwind.config.js
├── tsconfig.json
├── package.json
└── README.md
```

## 🗄 Database Schema

### User Table
```sql
CREATE TABLE "User" (
  id          String      PRIMARY KEY
  email       String      UNIQUE NOT NULL
  password    String      NOT NULL (hashed)
  firstName   String      NOT NULL
  lastName    String      NOT NULL
  phone       String
  role        Role        (STUDENT, ADMIN, INSTRUCTOR)
  status      Status      (ACTIVE, INACTIVE, SUSPENDED)
  createdAt   DateTime    DEFAULT now()
  updatedAt   DateTime
)
```

### Course Table
```sql
CREATE TABLE "Course" (
  id          String      PRIMARY KEY
  title       String      NOT NULL
  description String
  price       Float       NOT NULL
  duration    Int         (in weeks)
  category    String
  instructor  String
  published   Boolean     DEFAULT false
  createdAt   DateTime    DEFAULT now()
  updatedAt   DateTime
)
```

### Enrollment Table
```sql
CREATE TABLE "Enrollment" (
  id          String      PRIMARY KEY
  userId      String      FOREIGN KEY
  courseId    String      FOREIGN KEY
  status      EnrollmentStatus (ACTIVE, COMPLETED, DROPPED)
  progress    Float       DEFAULT 0
  createdAt   DateTime    DEFAULT now()
  updatedAt   DateTime
)
```

## 🔐 Security Features

- ✅ Password hashing with bcryptjs
- ✅ JWT token authentication
- ✅ Input validation with Zod
- ✅ SQL injection prevention via Prisma ORM
- ✅ CORS configuration
- ✅ Environment variable protection
- ✅ Session management
- ✅ Rate limiting ready

## 📝 Environment Variables

Create `.env.local`:

```env
# Database
DATABASE_URL="postgresql://username:password@localhost:5432/skill_sync"

# NextAuth
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="your-super-secret-key-change-in-production"

# Email (Optional)
EMAIL_HOST="smtp.gmail.com"
EMAIL_PORT="587"
EMAIL_USER="your-email@gmail.com"
EMAIL_PASSWORD="your-app-password"
EMAIL_FROM="noreply@skillsyncacademy.com"

# Application
NODE_ENV="development"
APP_NAME="Skill Sync Academy"
APP_URL="http://localhost:3000"
```

## 🗄 Database Setup

### PostgreSQL Installation

**macOS (Homebrew)**
```bash
brew install postgresql
brew services start postgresql
createdb skill_sync
```

**Windows**
Download from: https://www.postgresql.org/download/windows/

**Linux (Ubuntu)**
```bash
sudo apt-get install postgresql postgresql-contrib
sudo systemctl start postgresql
```

### Run Migrations

```bash
# Create and run migrations
npx prisma migrate dev --name init

# Seed sample data
npx prisma db seed

# Open Prisma Studio (database GUI)
npx prisma studio
```

## 🧪 Testing

```bash
# Development server
npm run dev

# Build for production
npm run build

# Start production server
npm run start

# Lint code
npm run lint

# Seed database
npm run prisma:seed
```

## 👤 User Roles

### Student Role
- Access own dashboard
- View available courses
- Enroll in courses
- Track progress
- Submit assignments
- Download certificates

### Admin Role
- Access admin dashboard
- Create & edit courses
- View all students
- Manage enrollments
- View analytics
- Send bulk messages

## 🚀 Deployment

### Deploy to Vercel (Recommended)

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel

# Set environment variables
vercel env add DATABASE_URL
vercel env add NEXTAUTH_SECRET
vercel env add NEXTAUTH_URL
```

### Deploy with Docker

```bash
# Build image
docker build -t skill-sync-academy .

# Run container
docker run -p 3000:3000 skill-sync-academy
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

MIT License - See LICENSE file for details

## 📞 Support

For issues and questions:
- 📧 Email: support@skillsyncacademy.com
- 🐛 GitHub Issues: [Create Issue](https://github.com/Dzunani95/skill-sync-academy/issues)
- 💬 Discussions: [GitHub Discussions](https://github.com/Dzunani95/skill-sync-academy/discussions)

## 🎓 Next Steps

- [ ] Set up PostgreSQL database
- [ ] Configure environment variables
- [ ] Run database migrations
- [ ] Create admin account
- [ ] Add sample courses
- [ ] Invite test students
- [ ] Test authentication flow
- [ ] Configure email notifications
- [ ] Set up payment integration
- [ ] Deploy to production

---

**Made with ❤️ for South African Youth** 🇿🇦

*Connecting Skills to the Future* 🚀
