# 🚀 Golden CI/CD Node.js

Production-ready Node.js Express API with automated CI/CD pipeline, Docker containerization, and Docker Hub integration.

## 📋 Architecture

```
golden-cicd-nodejs/
├── src/
│   └── index.js              # Express application
├── tests/
│   └── api.test.js           # Jest test suite
├── .github/workflows/
│   └── ci-cd.yml             # GitHub Actions pipeline
├── Dockerfile                # Multi-stage Docker build
├── package.json              # Dependencies and scripts
├── jest.config.js            # Jest configuration
├── .eslintrc.json            # ESLint configuration
├── .env.example              # Environment variables template
└── README.md
```

## 🔄 CI/CD Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                         PUSH TO MAIN                            │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│  STEP 1: Checkout Code & Setup Node.js 20                      │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│  STEP 2: Install Dependencies (npm ci)                         │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│  STEP 3: Run Tests (Jest)                                      │
│  ❌ FAIL → Pipeline stops                                      │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│  STEP 4: Build Docker Image                                    │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│  STEP 5: Run Container & Verify Health                         │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│  STEP 6: Push to Docker Hub                                    │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│  ✅ PIPELINE COMPLETE                                           │
└─────────────────────────────────────────────────────────────────┘
```

## 🏃 Run Locally

### Prerequisites
- Node.js 20+
- npm

### Steps

1. Clone repository:
```bash
git clone https://github.com/YOUR_USERNAME/golden-cicd-nodejs.git
cd golden-cicd-nodejs
```

2. Install dependencies:
```bash
npm install
```

3. Set environment variables:
```bash
cp .env.example .env
```

4. Run application:
```bash
npm start
```

5. Test endpoints:
```bash
curl http://localhost:3000/
curl http://localhost:3000/health
```

6. Run tests:
```bash
npm test
```

7. Development mode (with auto-reload):
```bash
npm run dev
```

## 🐳 Run with Docker

### Build and run:
```bash
docker build -t golden-cicd-nodejs .
docker run -d --name nodejs-app -p 3000:3000 -e APP_ENV=local golden-cicd-nodejs
```

### Verify:
```bash
curl http://localhost:3000/health
```

### Stop:
```bash
docker stop nodejs-app
docker rm nodejs-app
```

## 🐳 Docker Hub

### Pull from Docker Hub:
```bash
docker pull ninad04/golden-cicd-nodejs:latest
docker run -d -p 3000:3000 ninad04/golden-cicd-nodejs:latest
```

## 📊 API Endpoints

| Endpoint | Method | Description | Response |
|----------|--------|-------------|----------|
| `/` | GET | Root endpoint | `{"message": "...", "environment": "...", "version": "..."}` |
| `/health` | GET | Health check | `{"status": "OK", "environment": "...", "uptime": ..., "timestamp": "..."}` |

## 🧪 Testing

```bash
# Run all tests
npm test

# Run tests in watch mode
npm run test:watch

# Run with coverage
npm test -- --coverage
```

## 🔧 Linting

```bash
# Check for issues
npm run lint

# Fix issues automatically
npm run lint:fix
```

## 🔐 Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `APP_ENV` | `local` | Environment name (local/ci/production) |
| `PORT` | `3000` | Application port |
| `NODE_ENV` | `development` | Node environment |

## 📦 Docker Image Details

- Base: `node:20-alpine`
- Size: ~120MB (optimized)
- Port: 3000
- Runtime: Node.js 20

## ☁️ Deploy to EC2 (Future)

The repository includes commented EC2 deployment code. To enable:

1. Add GitHub Secrets: `EC2_HOST`, `EC2_USER`, `EC2_SSH_KEY`
2. Uncomment EC2 job in `.github/workflows/ci-cd.yml`
3. Push changes

## 🔧 Scripts

| Script | Description |
|--------|-------------|
| `npm start` | Start production server |
| `npm run dev` | Start development server with auto-reload |
| `npm test` | Run tests with Jest |
| `npm run test:watch` | Run tests in watch mode |
| `npm run lint` | Check code quality |
| `npm run lint:fix` | Fix linting issues |

## 🐛 Troubleshooting

### Port already in use
```bash
# Windows
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# Linux/Mac
lsof -ti:3000 | xargs kill
```

### Tests fail
```bash
npm test -- --verbose
```

### Docker issues
```bash
docker logs nodejs-app
```

## 📝 License

MIT

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Commit changes
4. Push to branch
5. Open Pull Request

---

Built with ❤️ using Node.js, Express, Docker, and GitHub Actions
