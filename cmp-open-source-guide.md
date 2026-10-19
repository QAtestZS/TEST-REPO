# CMP Open Source Implementation Overview

Below you'll find the comprehensive tables and instructions covered in our discussion, tailored for building a Consent Management Platform (CMP) in React + Vite + Tailwind CSS (frontend) and Django + PostgreSQL (backend) with REST API and JWT authentication. This includes all open-source packages, their usage, setup scripts, directory mapping, and feature-component associations.

---

## 1. Complete Package List for CMP Platform

### Backend Packages (Django + PostgreSQL)

| Package/Tool | Version | Purpose | Category | Installation Command |
|--------------|---------|---------|----------|---------------------|
| Django | 4.2+ | Web framework | Core Backend | pip install django |
| djangorestframework | 3.14+ | REST API framework | API Layer | pip install djangorestframework |
| psycopg2-binary | 2.9+ | PostgreSQL adapter | Database | pip install psycopg2-binary |
| django-cors-headers | 4.0+ | CORS handling | API Security | pip install django-cors-headers |
| djangorestframework-simplejwt | 5.2+ | JWT authentication | Authentication | pip install djangorestframework-simplejwt |
| presidio-analyzer | 2.2+ | PII detection/discovery | PII Discovery | pip install presidio-analyzer |
| presidio-anonymizer | 2.2+ | PII masking/anonymization | Data Masking | pip install presidio-anonymizer |
| spacy | 3.7+ | NLP engine for PII detection | PII Discovery | pip install spacy |
| en_core_web_lg | 3.7+ | English language model | PII Discovery | python -m spacy download en_core_web_lg |
| faker | 19.6+ | Generate fake/synthetic data | Data Masking | pip install faker |
| celery | 5.3+ | Async task queue (optional) | Background Jobs | pip install celery |
| redis | 4.6+ | Cache & message broker | Performance | pip install redis |
| python-decouple | 3.8+ | Environment variables | Configuration | pip install python-decouple |
| gunicorn | 20.1+ | Production WSGI server | Deployment | pip install gunicorn |
| pytest | 7.4+ | Testing framework | Testing | pip install pytest |
| pytest-django | 4.5+ | Django testing utilities | Testing | pip install pytest-django |

### Frontend Packages (React + Vite)

| Package/Tool | Version | Purpose | Category | Installation Command |
|--------------|---------|---------|----------|---------------------|
| react | 18.2+ | UI library | Core Frontend | npm install react |
| react-dom | 18.2+ | React DOM renderer | Core Frontend | npm install react-dom |
| vite | 4.4+ | Build tool & dev server | Build Tool | npm install vite |
| @vitejs/plugin-react | 4.0+ | React plugin for Vite | Build Tool | npm install @vitejs/plugin-react |
| tailwindcss | 3.3+ | Utility-first CSS framework | Styling | npm install tailwindcss |
| postcss | 8.4+ | CSS processing | Styling | npm install postcss |
| autoprefixer | 10.4+ | Auto-prefix CSS | Styling | npm install autoprefixer |
| react-router-dom | 6.14+ | Client-side routing | Navigation | npm install react-router-dom |
| axios | 1.4+ | HTTP client for API calls | API Integration | npm install axios |
| lucide-react | 0.263+ | Icon library | UI Components | npm install lucide-react |
| js-cookie | 3.0+ | Cookie management | Consent Storage | npm install js-cookie |
| recharts | 2.7+ | Analytics charts (optional) | Consent Analytics | npm install recharts |
| date-fns | 2.30+ | Date manipulation | Utilities | npm install date-fns |

### DevOps & Deployment

| Package/Tool | Version | Purpose | Category | Installation Command |
|--------------|---------|---------|----------|---------------------|
| docker | 24+ | Containerization | Deployment | System package |
| docker-compose | 2.20+ | Multi-container orchestration | Deployment | System package |
| nginx | 1.24+ | Reverse proxy & static files | Web Server | System package |
| postgresql | 15+ | Database server | Database | System package |

### Optional Enhancement Packages

| Package/Tool | Version | Purpose | Category | Installation Command |
|--------------|---------|---------|----------|---------------------|
| django-filter | 23.2+ | Advanced filtering for APIs | API Enhancement | pip install django-filter |
| drf-yasg | 1.21+ | API documentation (Swagger) | Documentation | pip install drf-yasg |
| django-debug-toolbar | 4.1+ | Development debugging | Development | pip install django-debug-toolbar |
| sentry-sdk | 1.28+ | Error tracking | Monitoring | pip install sentry-sdk |
| react-query | 4.32+ | Server state management | Frontend State | npm install @tanstack/react-query |
| zustand | 4.3+ | Client state management | Frontend State | npm install zustand |

---

## 2. CMP Core Features Implementation

| Feature | Backend Packages | Frontend Packages | Custom Code Location |
|---------|------------------|-------------------|---------------------|
| Consent Banners | Django REST, JWT | React, Tailwind CSS | ConsentBanner.jsx, consent-widget.js |
| Auto Script Blocking | Django, Custom middleware | JavaScript (vanilla) | consent-widget.js, middleware |
| Consent Capture | Django REST, PostgreSQL | Axios, React | views.py, ConsentBanner.jsx |
| Preference Handling | Django models, REST API | React Router, Axios | PreferenceCenter.jsx, views.py |
| Consent Collection | Django ORM, PostgreSQL | React forms, Axios | models.py, serializers.py |
| Audit Logs | Django models, PostgreSQL | Recharts (for visualization) | ConsentAuditLog model |
| Consent Analytics | Django aggregation queries | Recharts, React | Custom analytics views |
| PII Detection | presidio-analyzer, spacy | N/A (backend only) | pii_discovery.py |
| Data Masking | presidio-anonymizer, faker | N/A (backend only) | data_masking.py |
| JWT Authentication | djangorestframework-simplejwt | Axios interceptors | api.js, Django settings |

---

## 3. Complete Installation Script

### Backend Setup Script

Create `backend/setup.sh`:

```bash
#!/bin/bash

# Create virtual environment
python3 -m venv venv
source venv/bin/activate

# Install all backend packages
pip install --upgrade pip

# Core Django packages
pip install django==4.2.0
pip install djangorestframework==3.14.0
pip install psycopg2-binary==2.9.6
pip install django-cors-headers==4.0.0
pip install djangorestframework-simplejwt==5.2.2

# PII Discovery & Masking
pip install presidio-analyzer==2.2.33
pip install presidio-anonymizer==2.2.33
pip install spacy==3.7.2
pip install faker==19.6.2

# Download spaCy model
python -m spacy download en_core_web_lg

# Utilities
pip install python-decouple==3.8
pip install celery==5.3.0
pip install redis==4.6.0

# Production
pip install gunicorn==20.1.0

# Development & Testing
pip install pytest==7.4.0
pip install pytest-django==4.5.2
pip install django-debug-toolbar==4.1.0

# Optional enhancements
pip install django-filter==23.2
pip install drf-yasg==1.21.7

# Save requirements
pip freeze > requirements.txt

echo "Backend setup complete!"
```

### Frontend Setup Script

Create `frontend/setup.sh`:

```bash
#!/bin/bash

# Initialize Vite + React project (if not already done)
# npm create vite@latest . -- --template react

# Install core packages
npm install react@18.2.0 react-dom@18.2.0

# Install Vite
npm install vite@4.4.0 @vitejs/plugin-react@4.0.0

# Install Tailwind CSS
npm install -D tailwindcss@3.3.2 postcss@8.4.24 autoprefixer@10.4.14

# Install routing and HTTP
npm install react-router-dom@6.14.0 axios@1.4.0

# Install UI libraries
npm install lucide-react@0.263.1

# Install utilities
npm install js-cookie@3.0.5 date-fns@2.30.0

# Optional: Analytics charts
npm install recharts@2.7.2

# Optional: State management
npm install zustand@4.3.9
npm install @tanstack/react-query@4.32.0

# Initialize Tailwind
npx tailwindcss init -p

echo "Frontend setup complete!"
```

---

## 4. Directory Structure with Packages

```
consent-management-platform/
├── backend/
│   ├── requirements.txt          # All Python packages
│   ├── setup.sh                  # Backend setup script
│   ├── manage.py
│   ├── .env
│   ├── Dockerfile
│   ├── project/
│   │   ├── settings.py           # Uses: Django, CORS, JWT, REST
│   │   ├── urls.py
│   │   └── wsgi.py               # Uses: gunicorn
│   └── consent_management/
│       ├── models.py              # Uses: Django ORM, PostgreSQL
│       ├── serializers.py         # Uses: DRF
│       ├── views.py               # Uses: DRF, JWT
│       ├── urls.py
│       ├── admin.py
│       ├── services/
│       │   ├── pii_discovery.py   # Uses: presidio-analyzer, spacy
│       │   └── data_masking.py    # Uses: presidio-anonymizer, faker
│       ├── middleware/
│       │   └── consent_enforcement.py  # Custom middleware
│       ├── migrations/
│       └── management/
│           └── commands/
│               └── seed_consent_data.py
│
├── frontend/
│   ├── package.json               # All NPM packages
│   ├── setup.sh                   # Frontend setup script
│   ├── vite.config.js             # Uses: Vite
│   ├── tailwind.config.js         # Uses: Tailwind CSS
│   ├── postcss.config.js
│   ├── .env
│   ├── index.html
│   ├── src/
│   │   ├── main.jsx               # Uses: React, React-DOM
│   │   ├── App.jsx                # Uses: React Router
│   │   ├── components/
│   │   │   ├── consent/
│   │   │   │   ├── ConsentBanner.jsx       # Uses: React, Axios, Lucide
│   │   │   │   ├── PreferenceCenter.jsx    # Uses: React, Axios, Lucide
│   │   │   │   ├── ConsentAnalytics.jsx    # Uses: Recharts
│   │   │   │   └── AuditLogViewer.jsx      # Uses: React, date-fns
│   │   │   └── common/
│   │   │       └── ProtectedRoute.jsx      # JWT protection
│   │   ├── services/
│   │   │   ├── api.js             # Uses: Axios (JWT interceptors)
│   │   │   └── consent.js         # Consent service layer
│   │   ├── hooks/
│   │   │   └── useConsent.js      # Custom React hook
│   │   └── utils/
│   │       ├── cookies.js         # Uses: js-cookie
│   │       └── storage.js
│   └── public/
│       └── consent-widget.js      # Vanilla JS (no dependencies)
│
├── docker-compose.yml             # Uses: Docker, PostgreSQL, Redis
└── README.md
```

---

## 5. Quick Start Commands

### Complete Setup (One-Time)

```bash
# Backend
cd backend
chmod +x setup.sh
./setup.sh

# Apply migrations
python manage.py makemigrations consent_management
python manage.py migrate
python manage.py seed_consent_data

# Frontend
cd ../frontend
chmod +x setup.sh
./setup.sh

# Initialize Tailwind
npx tailwindcss init -p
```

### Development

```bash
# Terminal 1 - Backend
cd backend
source venv/bin/activate
python manage.py runserver

# Terminal 2 - Frontend
cd frontend
npm run dev
```

### Production with Docker

```bash
docker-compose up -d
```

---

## Summary

You now have a unified, open-source stack and explicit instructions for building, deploying, and scaling a modern CMP with PII detection and data masking. All mapped dependencies ensure smooth integration between Django/PostgreSQL backend and React/Vite/Tailwind frontend - with high extensibility for analytics, consent banners, auto script blocking, audit logs, and privacy compliance workflows.
