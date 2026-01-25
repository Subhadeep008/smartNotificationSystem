# Smart Notification System for Preventive and Predictive Maintenance in Manufacturing (SH10)

## Overview

This is a full-stack web application designed for smart maintenance management in manufacturing environments. The system provides preventive and predictive maintenance scheduling with real-time notifications, role-based access control, and comprehensive reporting capabilities.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React.js with TypeScript
- **Styling**: Tailwind CSS with shadcn/ui component library
- **State Management**: React Query (TanStack Query) for server state
- **Routing**: Wouter for client-side routing
- **Form Management**: React Hook Form with Zod validation
- **Build Tool**: Vite

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript (ESM modules)
- **Authentication**: Passport.js with local strategy and sessions
- **Session Store**: PostgreSQL-based session storage

### Database Architecture
- **Database**: PostgreSQL (via Neon serverless)
- **ORM**: Drizzle ORM with Drizzle Kit for migrations
- **Connection**: Neon serverless client with WebSocket support

## Key Components

### Authentication System
- **Strategy**: Session-based authentication using Passport.js
- **Password Security**: Scrypt hashing with salt
- **Role-based Access**: Three user roles (admin, supervisor, staff)
- **Session Management**: PostgreSQL session store with 24-hour expiry

### Database Schema
- **Users**: Role-based user management with departments
- **Machines**: Machine registry with runtime/overload thresholds
- **Maintenance Tasks**: Scheduled tasks with status tracking
- **Alerts**: Real-time alert system with severity levels
- **Power Shutdowns**: TNEB power shutdown scheduling
- **Maintenance Logs**: Historical maintenance records
- **Notifications**: System notification tracking

### Notification Services
- **Email**: NodeMailer for email notifications
- **Real-time Alerts**: Alert system for threshold breaches
- **Scheduled Notifications**: Cron-based scheduled notifications

### Reporting System
- **Formats**: PDF and CSV report generation
- **Types**: Maintenance logs, alert summaries, power shutdown history
- **Filtering**: Date range, machine, and status-based filtering

### Scheduled Services
- **Cron Jobs**: Automated maintenance checks and notifications
- **Maintenance Monitoring**: Hourly checks for upcoming tasks
- **Runtime Tracking**: Periodic machine runtime updates

## Data Flow

1. **User Authentication**: Login → Session creation → Role-based access
2. **Machine Management**: Admin creates machines → Sets thresholds → Monitors status
3. **Task Scheduling**: Admin/Supervisor schedules maintenance → Assigns to staff
4. **Alert Generation**: System monitors thresholds → Generates alerts → Sends notifications
5. **Task Execution**: Staff receives notifications → Completes tasks → Updates status
6. **Reporting**: System generates reports → Exports to PDF/CSV

## External Dependencies

### Core Dependencies
- **@neondatabase/serverless**: PostgreSQL database connection
- **drizzle-orm**: Database ORM and query builder
- **passport**: Authentication middleware
- **nodemailer**: Email notification service
- **node-cron**: Scheduled task management
- **pdfkit**: PDF report generation
- **csv-writer**: CSV export functionality

### UI Dependencies
- **@radix-ui/***: Comprehensive UI component primitives
- **@tanstack/react-query**: Server state management
- **recharts**: Data visualization charts
- **react-hook-form**: Form management
- **zod**: Schema validation
- **tailwindcss**: Utility-first CSS framework

### Development Dependencies
- **vite**: Build tool and dev server
- **typescript**: Type safety
- **tsx**: TypeScript execution
- **esbuild**: JavaScript bundling

## Deployment Strategy

### Development
- **Server**: TSX for TypeScript execution in development
- **Client**: Vite dev server with HMR
- **Database**: Drizzle Kit for schema management

### Production
- **Build Process**: 
  1. Frontend: Vite builds React app to `dist/public`
  2. Backend: esbuild bundles server to `dist/index.js`
- **Serving**: Express serves static files from `dist/public`
- **Database**: Drizzle migrations via `db:push` command
- **Environment**: Production-specific session security settings

### Environment Variables Required
- `DATABASE_URL`: PostgreSQL connection string
- `SESSION_SECRET`: Session encryption key
- `SMTP_HOST`, `SMTP_PORT`, `SMTP_USER`, `SMTP_PASS`: Email configuration
- `NODE_ENV`: Environment setting

### File Structure
- `/client`: React frontend application
- `/server`: Express backend API
- `/shared`: Shared TypeScript schemas and types
- `/dist`: Production build output
- `/migrations`: Database migration files