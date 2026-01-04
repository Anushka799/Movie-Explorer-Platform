# Movie Explorer Platform

A comprehensive full-stack web application for exploring movies, actors, directors, and genres. This project demonstrates modern web development practices using **FastAPI** (backend) and **Vue.js** (frontend), designed for film enthusiasts to browse and discover movie information.

> **Note**: This is a technical assessment project showcasing full-stack development capabilities.

## 🎯 Features

- **Movie Browse & Search**: View movies with filtering by genre, director, actor, and release year
- **Detailed Movie Pages**: Complete information including cast, genres, director, and synopsis
- **Actor Profiles**: Browse actor filmographies and biographies
- **Director Profiles**: Explore director filmographies and career statistics
- **Server-Side Filtering**: All filtering operations performed on the backend for optimal performance
- **Responsive Design**: Modern, mobile-friendly interface built with Tailwind CSS
- **RESTful API**: Well-documented API with OpenAPI/Swagger specification

## 🏗️ Architecture

### Backend (FastAPI)
- **Language**: Python 3.11
- **Framework**: FastAPI
- **Database**: SQLite (local)
- **ORM**: SQLAlchemy
- **API Documentation**: Swagger UI / OpenAPI
- **Testing**: Pytest

### Frontend (Vue.js)
- **Framework**: Vue 3 with Composition API
- **Language**: TypeScript
- **Build Tool**: Vite
- **Styling**: Tailwind CSS
- **State Management**: Pinia
- **Routing**: Vue Router
- **Testing**: Vitest + Vue Test Utils

## 📁 Project Structure

```
movie-explorer-platform/
├── backend/                 # FastAPI backend application
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py         # FastAPI app entry point
│   │   ├── database.py     # Database configuration
│   │   ├── models.py       # SQLAlchemy models
│   │   ├── schemas.py      # Pydantic schemas
│   │   ├── crud.py         # Database operations
│   │   ├── seed_data.py    # Sample data seeding
│   │   └── routers/        # API route modules
│   │       ├── movies.py
│   │       ├── actors.py
│   │       ├── directors.py
│   │       └── genres.py
│   ├── requirements.txt    # Python dependencies
│   ├── run.py             # Application runner
│   ├── test_main.py       # API tests
│   └── Dockerfile         # Backend Docker configuration
├── frontend/               # Vue.js frontend application
│   ├── src/
│   │   ├── components/    # Reusable Vue components
│   │   ├── views/         # Page components
│   │   ├── stores/        # Pinia state management
│   │   ├── services/      # API service layer
│   │   ├── types/         # TypeScript type definitions
│   │   ├── router/        # Vue Router configuration
│   │   ├── main.ts        # App entry point
│   │   └── style.css      # Global styles
│   ├── package.json       # Node.js dependencies
│   ├── vite.config.ts     # Vite configuration
│   ├── tailwind.config.js # Tailwind CSS configuration
│   ├── vitest.config.ts   # Testing configuration
│   ├── nginx.conf         # Nginx configuration for production
│   └── Dockerfile         # Frontend Docker configuration
├── docker-compose.yml     # Multi-container orchestration
└── README.md             # This file
```

## 🚀 Quick Start

### Prerequisites

- **Docker & Docker Compose** (recommended for easy setup)
- **OR** Node.js 18+ and Python 3.11+ (for local development)

### Option 1: Docker Setup (Recommended)



1. **Start the application**:
   ```bash
   docker-compose up --build
   ```

2. **Access the application**:
   - **Frontend**: http://localhost:3000
   - **Backend API**: http://localhost:8000
   - **API Documentation**: http://localhost:8000/docs

   > 🎬 **Note**: The database automatically populates with sample movies on first startup!

### Option 2: Local Development Setup

#### Backend Setup

1. **Navigate to backend directory**:
   ```bash
   cd backend
   ```

2. **Create virtual environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the backend**:
   ```bash
   python run.py
   ```

The backend will be available at http://localhost:8000

#### Frontend Setup

1. **Navigate to frontend directory** (in a new terminal):
   ```bash
   cd frontend
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Start development server**:
   ```bash
   npm run dev
   ```

The frontend will be available at http://localhost:5173

> 🎬 **Note**: The backend automatically seeds the database with sample movies on startup!

## 📖 API Documentation

The API follows RESTful conventions and includes comprehensive documentation:

- **Interactive Documentation**: http://localhost:8000/docs (Swagger UI)
- **Alternative Documentation**: http://localhost:8000/redoc (ReDoc)

### Core Endpoints

#### Movies
- `GET /api/movies/` - List movies with optional filtering
- `GET /api/movies/{id}` - Get movie details
- `POST /api/movies/` - Create new movie (admin)

**Filtering Parameters**:
- `genre_id`: Filter by genre
- `director_id`: Filter by director
- `actor_id`: Filter by actor
- `release_year`: Filter by release year

#### Actors
- `GET /api/actors/` - List actors with optional filtering
- `GET /api/actors/{id}` - Get actor profile with filmography
- `POST /api/actors/` - Create new actor (admin)

#### Directors
- `GET /api/directors/` - List directors
- `GET /api/directors/{id}` - Get director profile with filmography
- `POST /api/directors/` - Create new director (admin)

#### Genres
- `GET /api/genres/` - List all genres
- `GET /api/genres/{id}` - Get specific genre
- `POST /api/genres/` - Create new genre (admin)

### Example API Calls

```bash
# Get all movies
curl "http://localhost:8000/api/movies/"

# Get movies by genre
curl "http://localhost:8000/api/movies/?genre_id=1"

# Get movies by director and year
curl "http://localhost:8000/api/movies/?director_id=1&release_year=2010"

# Get specific movie details
curl "http://localhost:8000/api/movies/1"

# Get actor profile
curl "http://localhost:8000/api/actors/1"
```

## 🧪 Testing

### Backend Testing

Run backend tests:
```bash
cd backend
pytest test_main.py -v
```

Run with coverage:
```bash
pytest test_main.py --cov=app --cov-report=html
```

### Frontend Testing

Run frontend tests:
```bash
cd frontend
npm run test
```

Run tests with UI:
```bash
npm run test:ui
```

### Linting

Backend linting:
```bash
cd backend
flake8 app/
```

Frontend linting:
```bash
cd frontend
npm run lint
```

## 🗄️ Database

The application uses SQLite for simplicity, with the following schema:

### Tables
- **movies**: Movie information (title, year, synopsis, duration)
- **actors**: Actor profiles (name, birth year, bio)
- **directors**: Director profiles (name, birth year, bio)
- **genres**: Movie genres (name, description)
- **movie_actors**: Many-to-many relationship between movies and actors
- **movie_genres**: Many-to-many relationship between movies and genres

### Automatic Database Initialization
The application **automatically seeds the database** with sample data on first startup:

**Sample Data Included:**
- **5 Movies**: Inception, The Dark Knight, Pulp Fiction, La La Land, The Wolf of Wall Street
- **5 Directors**: Christopher Nolan, Quentin Tarantino, Steven Spielberg, Martin Scorsese, Greta Gerwig
- **8 Actors**: Leonardo DiCaprio, Margot Robbie, Christian Bale, Scarlett Johansson, Ryan Gosling, Emma Stone, Tom Hardy, Samuel L. Jackson
- **8 Genres**: Action, Drama, Comedy, Sci-Fi, Thriller, Romance, Horror, Adventure

**Smart Seeding**: The system checks if data already exists and only seeds empty databases, preventing duplicates on restart.

## 🎨 User Interface

The frontend provides a modern, responsive interface with:

- **Homepage**: Hero section with movie grid and filtering controls
- **Movie Detail Pages**: Complete movie information with cast and crew
- **Actor Profiles**: Filmographies and biographical information
- **Director Profiles**: Career statistics and directed movies
- **Responsive Design**: Optimized for desktop, tablet, and mobile devices

### Design System
- **Primary Colors**: Blue theme with accent colors
- **Typography**: Clear hierarchy with readable fonts
- **Components**: Consistent card-based layout
- **Interactions**: Smooth transitions and hover effects

## 🐳 Docker Configuration

### Development
```bash
# Start in development mode with hot reload
docker-compose up --build

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

### Production Deployment

For production deployment, consider:

1. **Environment Variables**: Use `.env` files for configuration
2. **Database**: Switch to PostgreSQL or MySQL for production
3. **Security**: Implement authentication and authorization
4. **Performance**: Add caching layer (Redis)
5. **Monitoring**: Integrate logging and monitoring tools

## 🔧 Configuration

### Backend Configuration
- Database URL can be configured in `backend/app/database.py`
- CORS settings configured in `backend/app/main.py`
- Server settings in `backend/run.py`
- **Database Seeding**: Automatic seeding controlled in `backend/app/seed_data.py`
  - Runs on every startup via `backend/run.py`
  - Skips seeding if data already exists
  - Can be run manually: `python -c "from app.seed_data import seed_database; seed_database()"`

### Frontend Configuration
- API base URL configured in `frontend/src/services/api.ts`
- Tailwind CSS customization in `frontend/tailwind.config.js`
- Build settings in `frontend/vite.config.ts`

## 🚦 Performance Considerations

- **Backend**: Database queries optimized with SQLAlchemy relationships
- **Frontend**: Component-based architecture with efficient state management
- **Caching**: Static assets cached with appropriate headers
- **Lazy Loading**: Route-based code splitting implemented

