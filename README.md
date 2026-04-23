# CloudGuard Academy 🛡️

An interactive web-based cybersecurity training platform featuring hands-on vulnerable labs with side-by-side code comparisons and a competitive leaderboard system.

## 🎯 Features

### Security Labs
- **SQL Injection (SQLi)** - Learn how to exploit and prevent SQL injection attacks
- **Cross-Site Scripting (XSS)** - Understand client-side injection vulnerabilities
- **Cross-Site Request Forgery (CSRF)** - Master token-based CSRF protection
- **Insecure Direct Object Reference (IDOR)** - Discover authorization bypass vulnerabilities

### Interactive Learning
- **Vulnerable & Secure Modes** - Compare vulnerable code with secure implementations
- **Live Sandbox** - Execute attacks in a safe environment with real-time feedback
- **Code Comparison** - Side-by-side code review with detailed explanations
- **Flag Submission System** - Verify successful exploits and earn points

### Gamification
- **Points System** - Earn points for each completed lab (100-150 pts per lab)
- **Leaderboard** - Compete globally with other security enthusiasts
- **Progress Tracking** - Monitor your learning journey

## 🏗️ Architecture

### Tech Stack
- **Frontend**: React 19 + TypeScript + Vite + Tailwind CSS + Lucide Icons
- **Backend**: Node.js + Express + TypeScript
- **Database**: SQLite + Prisma ORM
- **Authentication**: JWT (JSON Web Tokens)
- **Security**: bcryptjs, CORS, Helmet, Rate Limiting

### Project Structure
```
cloudguard-academy/
├── backend/                 # Node.js/Express API
│   ├── src/
│   │   ├── index.ts        # Server entry point
│   │   ├── seed.ts         # Database seeding
│   │   └── routes/
│   │       ├── auth.ts     # Auth endpoints (register/login)
│   │       └── labs.ts     # Lab endpoints (vulnerabilities + flags)
│   ├── prisma/
│   │   └── schema.prisma   # Database schema
│   ├── .env                # Environment variables
│   └── package.json
├── frontend/                # React/Vite app
│   ├── src/
│   │   ├── App.tsx         # Main app component with routing
│   │   ├── pages/          # Page components
│   │   │   ├── Login.tsx
│   │   │   ├── Register.tsx
│   │   │   ├── Dashboard.tsx
│   │   │   ├── LabSQLi.tsx
│   │   │   ├── LabXSS.tsx
│   │   │   ├── LabCSRF.tsx
│   │   │   ├── LabIDOR.tsx
│   │   │   └── Leaderboard.tsx
│   │   └── index.css       # Tailwind styles
│   └── package.json
├── docker-compose.yml      # PostgreSQL config (optional)
└── README.md              # This file
```

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ with npm
- SQLite3 (pre-bundled with Node)

### Installation

#### 1. Clone/Extract the Project
```bash
cd cloudguard-academy
```

#### 2. Backend Setup
```bash
cd backend

# Install dependencies
npm install

# Generate Prisma client
npx prisma generate

# Initialize the database
npx prisma db push

# Start the backend server
npm run dev
```

The backend will start at **http://localhost:5000**

#### 3. Frontend Setup (New Terminal)
```bash
cd frontend

# Install dependencies
npm install

# Start the development server
npm run dev
```

The frontend will start at **http://localhost:5173**

### Database Initialization

The database is automatically seeded on first backend startup. It creates:
- Base module: "Web Security Fundamentals"
- Ready for user registrations and lab submissions

To reset the database:
```bash
cd backend
rm dev.db  # Remove the SQLite file
npx prisma db push  # Recreate
npm run dev  # Restart backend to seed
```

## 📝 Available Scripts

### Backend
```bash
npm run dev      # Start dev server with ts-node
npm run build    # Compile TypeScript to dist/
npm start        # Run compiled JavaScript
```

### Frontend
```bash
npm run dev      # Start Vite dev server
npm run build    # Build for production
npm run preview  # Preview production build
npm run lint     # Run ESLint
```

## 🔐 Security Features

### Authentication
- **JWT Tokens** - Secure token-based authentication
- **Password Hashing** - bcryptjs with 10 salt rounds
- **Token Expiry** - 1-day token validity

### API Security
- **CORS** - Restricted to localhost:5173 in development
- **Helmet** - HTTP security headers
- **Rate Limiting** - 100 requests per 15 minutes per IP
- **Input Validation** - Required field checks

### Lab Vulnerabilities (Educational)
Each lab demonstrates both vulnerable and secure implementations:
1. **SQL Injection** - Raw queries vs. parameterized queries
2. **XSS** - Unescaped HTML vs. entity encoding
3. **CSRF** - No token validation vs. token verification
4. **IDOR** - Missing authorization vs. ownership checks

## 📚 Lab Details

### SQL Injection (100 points)
- **Objective**: Bypass login using SQL injection
- **Attack**: `' OR 1=1 --`
- **Defense**: Parameterized queries with Prisma ORM
- **Hint**: Comment syntax removes the password check

### Cross-Site Scripting (100 points)
- **Objective**: Execute JavaScript in the forum
- **Attack**: `<script>alert('XSS')</script>`
- **Defense**: HTML entity encoding
- **Hint**: Different vectors: script tags, img onerror, svg onload

### CSRF Attack (100 points)
- **Objective**: Transfer funds without CSRF token
- **Attack**: Submit form without token validation
- **Defense**: Unique, unpredictable token per session
- **Hint**: Tokens are single-use and rotated after success

### IDOR Attack (150 points)
- **Objective**: Access other users' documents
- **Attack**: Change DOC-001 → DOC-002
- **Defense**: Authorization checks on server-side
- **Hint**: Always verify object ownership before returning data

## 🎮 Gameplay

1. **Register or Login** - Create your account
2. **View Labs** - Browse available labs with points
3. **Choose Lab** - Select a vulnerability to study
4. **Switch Modes**:
   - **Vulnerable** - Exploit the vulnerability
   - **Secure** - See how to fix it
5. **Submit Flag** - Enter the flag shown on successful exploit
6. **Earn Points** - Points appear on your profile
7. **Check Leaderboard** - See your global ranking

## 🛠️ Environment Variables

### Backend (.env)
```
DATABASE_URL="file:./dev.db"
PORT=5000
JWT_SECRET=your-secret-key-here
```

### Frontend
No .env needed for development. API is hardcoded to `http://localhost:5000`

## 🧪 Testing the Application

### Test Account (After First Run)
1. Register: `test@example.com` / `password123`
2. Login with created account
3. Complete labs and submit flags
4. View progress on dashboard
5. Check leaderboard rankings

### Sample Flags
- SQLi: `FLAG{SQL_INJECTION_MASTER}`
- XSS: `FLAG{XSS_SCRIPT_INJECTOR}`
- CSRF: `FLAG{CSRF_FORGED_REQUEST}`
- IDOR: `FLAG{IDOR_ACCESS_VIOLATION}`

## 🐛 Troubleshooting

### Backend Won't Start
```bash
# Check if port 5000 is in use
lsof -i :5000

# Check Node version
node --version  # Should be 18+

# Reinstall dependencies
rm -rf node_modules package-lock.json
npm install
```

### Frontend Can't Connect to Backend
- Ensure backend is running on http://localhost:5000
- Check CORS settings in backend (backend/src/index.ts)
- Clear browser cache and localStorage

### Database Issues
```bash
# Reset database
cd backend
rm dev.db
npx prisma db push
```

### Port Already in Use
- Backend: Change PORT in .env (default: 5000)
- Frontend: Vite will use next available port (default: 5173)

## 📖 Educational Resources

### Web Security Topics Covered
- **Injection Attacks** - Understand SQL injection principles
- **Input Validation** - Why client-side validation is insufficient
- **Parameterized Queries** - Safe database access patterns
- **Output Encoding** - Preventing XSS through HTML escaping
- **State-Changing Requests** - CSRF protection mechanisms
- **Authorization** - Object-level access control
- **Token Management** - Secure token generation and validation

### Best Practices Demonstrated
✅ Use ORMs for database access
✅ Always validate server-side
✅ Escape user output
✅ Implement authorization checks
✅ Use strong authentication tokens
✅ Implement rate limiting
✅ Set security headers (Helmet)
✅ Never trust user input

## 🚀 Deployment (Optional)

### Build for Production
```bash
# Backend
cd backend
npm run build

# Frontend
cd frontend
npm run build
```

### Environment Configuration
Set proper environment variables for production:
- `DATABASE_URL` - Production database connection
- `JWT_SECRET` - Strong random secret
- `CORS_ORIGIN` - Production frontend URL
- `NODE_ENV=production`

## 📄 License

Educational Use Only - Use this project to learn cybersecurity concepts.

## 🤝 Contributing

Suggestions for improvements:
- Additional vulnerability labs
- More detailed explanations
- Custom challenges
- API documentation
- Expanded leaderboard features

---

**Happy Learning! 🎓 Remember: These labs are for educational purposes only. Never use these techniques on systems you don't own!**
