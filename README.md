CapOps Agent
CapOps Agent is an Intelligent BPO Assistant designed for Capgemini's internal operations. It autonomously resolves HR, Finance, and IT support queries. The system incorporates an advanced LangChain orchestrator with Claude API to provide intelligent routing, RAG over knowledge bases, live sentiment analysis, dynamic action execution, and a real-time React dashboard.

The architecture supports multiple channels (Web, Voice, Email) and seamlessly escalates consecutive frustrated queries to human agents with a summarized context package.

Architecture Diagram
       +---------------+       +-----------------+       
       | React Web App | <---> | NGINX Balancer  | <---> [ Port 8001 / 8002 ]
       | (Tailwind CSS)|       | (Round-Robin)   |       
       +-------^-------+       +-----------------+       
               |                        |
               v                        v
       +---------------+       +------------------+      +----------------+
       | Web Speech API|       | FastAPI Backend  | ---> |  ChromaDB RAG  |
       | (STT / Voice) |       | (Core Logic)     |      | (Knowledge KB) |
       +---------------+       +--------^---------+      +----------------+
                                        |
                            +-----------v-----------+
                            |  Anthropic Claude   |
                            |  API (Sonnet)       |
                            +-----------------------+
Features Complete
FastAPI Backend (main.py)
LangChain Orchestrator (agent.py)
ChromaDB RAG (rag.py)
Mock API Actions (actions.py)
Intent Classifier (nlu.py)
Sentiment Analysis (sentiment.py)
Session Management (session.py)
Security Rules (security.py)
Analytics Logging (analytics.py)
Claude Vision (vision.py)
4 Realistic Mined KBs + Mock Data
React Vite Web App
Live Dashboard + KPIs
Voice Input (Browser native)
Escalation Banner
NGINX Load Balancing
Recharts Visualization
Setup Instructions
Backend Start
cd backend
pip install -r requirements.txt
Terminal 1: uvicorn main:app --port 8001
Terminal 2: uvicorn main:app --port 8002
Frontend Start
cd frontend
npm install
npm run dev (or build to serve via Nginx: npm run build)
Nginx
Ensure Nginx is installed.
Copy nginx/nginx.conf and restart Nginx.
Sample cURL Requests
Chat Request:

curl -X POST http://localhost:80/api/chat \
-H "Content-Type: application/json" \
-d '{"message": "I need help resetting my SAP password. My ID is CG-1234."}'
Health Check:

curl http://localhost:80/api/health
Dashboard Stats:

curl http://localhost:80/api/dashboard/stats
Environment Variables
ANTHROPIC_API_KEY: API Key for Claude
WORKER_ID: Identifier for load balancing
PORT: Server port
CHROMA_DB_PATH: Vector DB persist location
LOG_PATH: Session logs path
