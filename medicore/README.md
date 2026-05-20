# MediCore — Healthcare Appointment Management System

A production-grade appointment booking system for multi-doctor clinics,
built with .NET 8, Angular 18, and Azure. Demonstrates clean architecture,
CQRS, and cloud-native deployment.

## Why I built this

I work with healthcare clients and wanted to build a portfolio
project that reflects the kinds of problems I solve daily — slot conflicts,
multi-tenant doctor management, audit trails, and async notifications.

## Tech stack

**Backend:** ASP.NET Core 8, Entity Framework Core 8, MediatR (CQRS),
FluentValidation, JWT auth, Serilog, xUnit

**Frontend:** Angular 18 (Signals, standalone components), Angular Material,
RxJS, Tailwind CSS

**Database:** Azure SQL Database / SQL Server

**Infrastructure:** Docker, Azure App Service, Azure Static Web Apps,
GitHub Actions CI/CD, SendGrid for transactional email

## Architecture

[insert architecture diagram here as an image]

The backend follows clean architecture with four layers:
- **Domain:** Entities, value objects, domain events
- **Application:** CQRS commands/queries via MediatR, business logic
- **Infrastructure:** EF Core, email service, blob storage
- **API:** Controllers, middleware, JWT auth

## Key features

- Multi-role authentication (Patient, Doctor, Admin) with JWT + refresh tokens
- Appointment booking with database-level slot conflict prevention
- Doctor availability rules (day-of-week, time windows, slot duration)
- Email notifications via SendGrid with audit trail
- Doctor specialization filtering and search
- Patient appointment history with status tracking

## Design decisions

A few choices worth explaining:

**Why CQRS via MediatR?** Separating reads from writes paid off when
adding appointment analytics — reporting queries don't pollute domain
logic, and the command pipeline gives a clean place to plug in validation,
logging, and authorization.

**Why a database-level unique constraint on appointment slots?**
Application-level checks have race conditions under concurrent bookings.
A unique index on (DoctorId, AppointmentDateTime) where Status != 'Cancelled'
guarantees no double-booking even if two requests arrive simultaneously.

**Why GUIDs as primary keys?** Forward compatibility — if this evolves
into microservices, GUIDs avoid the cross-service ID collision problem
that auto-incrementing integers create.

## Running locally

[step by step instructions]

## What's next

- [ ] Recurring appointments
- [ ] Telemedicine video integration (Azure Communication Services)
- [ ] Patient medical history module
- [ ] AI-powered booking assistant (Project #2 in my portfolio)

## License

MIT