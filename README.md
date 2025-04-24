# AI Calling Agent Platform

An advanced AI-powered calling platform that enables automated, multilingual voice interactions with customers using Indian mobile numbers.

## Features

### Admin Panel
- User authentication (mobile/email with OTP)
- Mobile number management for outbound calling
- Contact list management (CSV upload/manual entry)
- AI conversation script configuration
- Call monitoring and analytics
- Multilingual support (Hindi, Gujarati, English)
- Credit-based system

### AI Calling Agent
- Automated voice interactions
- Multi-language support
- Dynamic conversation flows
- Call recording and transcription
- Scheduled calling

### Super Admin Features
- Complete user management
- Credit limit control
- System-wide monitoring
- AI model management
- Real-time analytics dashboard

## Tech Stack

- **Backend**: FastAPI (Python)
- **Frontend**: Next.js (React)
- **Database**: PostgreSQL
- **Voice Processing**: Whisper + ElevenLabs
- **Call Integration**: Exotel/Twilio
- **Hosting**: AWS

## Project Structure

```
windsurf/
├── backend/                 # FastAPI backend
│   ├── app/
│   │   ├── api/            # API routes
│   │   ├── core/           # Core functionality
│   │   ├── models/         # Database models
│   │   └── services/       # Business logic
│   ├── requirements.txt
│   └── main.py
├── frontend/               # Next.js frontend
│   ├── src/
│   │   ├── components/     # React components
│   │   ├── pages/         # Next.js pages
│   │   └── styles/        # CSS styles
│   └── package.json
├── docker/                 # Docker configuration
└── docs/                   # Documentation
```

## Getting Started

### Backend (FastAPI)
1. Navigate to the backend directory:
   ```bash
   cd backend
   ```
2. Create and activate a virtual environment (optional but recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Run the backend server:
   ```bash
   uvicorn app.main:app --reload
   ```
5. API docs available at: [http://localhost:8000/docs](http://localhost:8000/docs)

### Frontend (Next.js)
1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Run the development server:
   ```bash
   npm run dev
   ```
4. Open [http://localhost:3000](http://localhost:3000) in your browser.

### Running Tests
- **Backend:**
  ```bash
  cd backend
  pytest
  ```
- **Frontend:**
  ```bash
  cd frontend
  npm test
  ```

### CI/CD
- Automated tests for both frontend and backend run on every push via GitHub Actions (see `.github/workflows/ci.yml`).

## API Endpoints
- Analytics: `/api/v1/analytics/summary`, `/agent-performance`, `/language-usage`
- Auth, Calls, Scripts, Users: See FastAPI docs `/docs`

## Environment Variables

- Copy the provided `.env.example` files to `.env` in the root, backend, and frontend directories.
- Edit these files to set your secrets and environment-specific values.
- **Do not commit `.env` files to version control.**

```bash
cp .env.example .env
cp backend/.env.example backend/.env
cp frontend/.env.example frontend/.env
```

## Deployment on AWS (ECS Example)

This project is ready for deployment on AWS ECS (Elastic Container Service) using Docker images for each service (backend, frontend, db, redis).

### 1. Build and Push Images
- Authenticate to your AWS ECR (Elastic Container Registry) and create repositories for each service.
- Build and tag Docker images:
  ```bash
  # Backend
  docker build -f docker/backend.Dockerfile -t <aws_account_id>.dkr.ecr.<region>.amazonaws.com/ai-caller-backend:latest .
  # Frontend
  docker build -f docker/frontend.Dockerfile -t <aws_account_id>.dkr.ecr.<region>.amazonaws.com/ai-caller-frontend:latest .
  ```
- Push images to ECR:
  ```bash
  docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/ai-caller-backend:latest
  docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/ai-caller-frontend:latest
  ```

### 2. Provision AWS Resources
- Create ECS Cluster, Task Definitions, and Services for backend and frontend.
- Use RDS for PostgreSQL and ElastiCache for Redis, or run containers for dev/testing.
- Set environment variables/secrets in ECS Task Definitions using AWS Secrets Manager or SSM Parameter Store.

### 3. Networking
- Set up a VPC, public/private subnets, and security groups.
- Use an Application Load Balancer (ALB) for routing to frontend/backend services.

### 4. Domain & SSL
- Point your domain to the ALB using Route 53.
- Use AWS Certificate Manager (ACM) for SSL certificates.

### 5. Monitoring & Scaling
- Enable CloudWatch logs for each service.
- Set up ECS service auto-scaling as needed.

---

For a full production deployment, see AWS ECS documentation and consider using Terraform or AWS CDK for infrastructure as code.

## License

[License information will be added here]
