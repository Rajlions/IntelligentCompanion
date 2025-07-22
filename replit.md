# Agent Management System

## Overview

This is a full-stack web application for creating and managing AI agents with layered processing capabilities. The system allows users to configure agents with multiple processing layers (input understanding, state tracking, planning, and output generation), conduct conversations with these agents, and debug their performance through detailed layer-by-layer analysis.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React with TypeScript
- **Styling**: Tailwind CSS with shadcn/ui component library
- **State Management**: TanStack React Query for server state
- **Routing**: Wouter for client-side navigation
- **Build Tool**: Vite with hot module replacement
- **Component System**: Modern component library with Radix UI primitives

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript with ES modules
- **Database ORM**: Drizzle ORM with PostgreSQL dialect
- **Database Provider**: Neon serverless PostgreSQL
- **API Integration**: OpenAI GPT-4o for AI processing
- **Session Management**: Express sessions with PostgreSQL storage

## Key Components

### Agent System
The application implements a layered agent architecture where each agent can have four types of processing layers:

1. **Input Understanding Layer**: Analyzes and categorizes incoming user messages
2. **State Tracker Layer**: Maintains conversation context and session state
3. **Planner Layer**: Determines appropriate responses and actions
4. **Output Layer**: Generates final responses to users

Each layer can be individually configured with custom system prompts and enabled/disabled as needed.

### Database Schema
- **agents**: Core agent definitions with name, use case, and status
- **agent_layers**: Layer configurations for each agent type
- **conversations**: Chat sessions between users and agents
- **messages**: Individual messages with optional debug information
- **agent_settings**: Agent-specific configuration (model, temperature, etc.)

### API Structure
RESTful API endpoints organized by resource:
- `/api/agents/*` - Agent management operations
- `/api/agents/:id/layers/*` - Layer configuration endpoints
- `/api/agents/:id/conversations/*` - Conversation management
- `/api/conversations/:id/messages/*` - Message handling

## Data Flow

1. **Agent Creation**: Users create agents with basic metadata (name, use case)
2. **Layer Configuration**: Each agent's processing layers are configured with custom prompts
3. **Conversation Initiation**: Users start conversations which create conversation records
4. **Message Processing**: User messages flow through enabled layers sequentially:
   - Input layer analyzes the message
   - State layer updates conversation context
   - Planner layer determines response strategy
   - Output layer generates the final response
5. **Debug Information**: Each layer's processing results are stored for debugging

## External Dependencies

### Core Dependencies
- **OpenAI API**: GPT-4o model for natural language processing
- **Neon Database**: Serverless PostgreSQL for data persistence
- **Radix UI**: Accessible component primitives
- **TanStack React Query**: Server state management and caching

### Development Tools
- **Drizzle Kit**: Database migrations and schema management
- **ESBuild**: Production build bundling
- **TypeScript**: Type safety and development experience
- **Tailwind CSS**: Utility-first styling

## Deployment Strategy

### Development Environment
- **Hot Reload**: Vite development server with HMR
- **Database**: Development database with push-based schema updates
- **API Proxy**: Vite proxy for seamless frontend-backend integration

### Production Build
- **Frontend**: Static assets built with Vite and served by Express
- **Backend**: Bundled with ESBuild for optimal performance
- **Database**: Production PostgreSQL with migration-based deployments
- **Environment Variables**: DATABASE_URL and OPENAI_API_KEY required

### Build Process
1. Frontend assets compiled to `dist/public`
2. Backend bundled to `dist/index.js`
3. Database schema deployed via Drizzle migrations
4. Single Node.js process serves both frontend and API

The application is designed for deployment on platforms like Replit, Vercel, or traditional Node.js hosting with PostgreSQL database support.