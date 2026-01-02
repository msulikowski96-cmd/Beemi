# MetabolicAI - Health Analysis Application

## Overview

MetabolicAI is a Polish-language health analysis web application that calculates metabolic metrics (BMI, BMR, TDEE) and provides AI-powered personalized health recommendations. The application uses a React frontend with an Express backend that integrates with OpenAI for generating health insights based on user biometric data.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Build Tool**: Vite for fast development and optimized production builds
- **Styling**: Tailwind CSS with PostCSS for utility-first styling
- **Charting**: Chart.js with react-chartjs-2 for data visualization (line charts for health metrics history)
- **Icons**: Lucide React for consistent iconography
- **Path Aliases**: Uses `@/` alias pointing to `./src` for cleaner imports

The frontend is a single-page application with state management using React hooks. It handles user input for health data (weight, height, age, gender, activity level) and displays calculated results along with AI-generated recommendations.

### Backend Architecture
- **Framework**: Express.js running on port 5001
- **Runtime**: Node.js with tsx for TypeScript execution
- **API Design**: RESTful endpoint at `/api/analyze` for health analysis

The backend serves as a proxy to OpenAI's API, constructing health-focused prompts with user biometric data and returning AI-generated analysis in Polish.

### Development Environment
- **Dev Server**: Vite dev server on port 5000 with proxy configuration to forward `/api` requests to Express backend on port 5001
- **Concurrent Execution**: `npm start` runs both frontend and backend simultaneously

### Core Calculations (Client-Side)
Located in `src/utils/calculators.ts`:
- **BMI**: Body Mass Index calculation
- **BMR**: Basal Metabolic Rate using Mifflin-St Jeor equation
- **TDEE**: Total Daily Energy Expenditure based on activity multiplier
- **BMI Category**: Classification (Niedowaga/Norma/Nadwaga/Otyłość)

### Data Flow
1. User enters biometric data in React form
2. Frontend calculates BMI, BMR, TDEE locally
3. Data sent to `/api/analyze` endpoint
4. Backend constructs prompt and queries OpenAI
5. AI response returned to frontend for display

### Pre-configured Integrations (`.replit_integration_files/`)
The repository includes scaffolding for additional Replit AI integrations that are not yet active in the main application:
- **Chat**: Persistent conversation storage with Drizzle ORM (PostgreSQL)
- **Image**: OpenAI image generation endpoints
- **Batch**: Rate-limited batch processing utilities

These integrations require database setup (Drizzle with PostgreSQL) before activation.

## External Dependencies

### AI Services
- **OpenAI API**: Used via Replit AI Integrations proxy
  - Environment Variables: `AI_INTEGRATIONS_OPENAI_API_KEY`, `AI_INTEGRATIONS_OPENAI_BASE_URL`
  - Model: `gpt-5.1` for health analysis text generation
  - Model: `gpt-image-1` available for image generation (scaffolded)

### Database (Scaffolded, Not Active)
- **Drizzle ORM**: Schema defined for conversations and messages tables
- **PostgreSQL**: Target database for chat persistence
- **Zod**: Schema validation for database inserts

### Key NPM Packages
- `openai`: Official OpenAI Node.js client
- `chart.js` / `react-chartjs-2`: Health metrics visualization
- `clsx` / `tailwind-merge`: Utility class management
- `tsx`: TypeScript execution for backend