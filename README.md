
<div align="center">

# SocioStruct

**Automated Community Operations Engine for FAST University societies**

A full-stack event management system that tracks user participation and community workflows, from society setup to event and competition registration, in one place.

![Node.js](https://img.shields.io/badge/Node.js-Express-339933?logo=node.js&logoColor=white)
![EJS](https://img.shields.io/badge/Views-EJS-B4CA65)
![MySQL](https://img.shields.io/badge/Database-MySQL-4479A1?logo=mysql&logoColor=white)
![Sequelize](https://img.shields.io/badge/ORM-Sequelize-52B0E7?logo=sequelize&logoColor=white)
![Bootstrap](https://img.shields.io/badge/UI-Bootstrap%205-7952B3?logo=bootstrap&logoColor=white)

</div>

---

## Table of Contents

- [About the Project](#about-the-project)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [System Design](#system-design)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Route Overview](#route-overview)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [Authors](#authors)

---

## About the Project

University societies often track events, registrations and team rosters through spreadsheets, forms and chat groups. This is slow, error-prone and hard to audit.

**SocioStruct** replaces those manual processes with a single full-stack web application that automates event management and tracks participation and community workflows. Students can browse societies and register for events and competitions. Administrators get a management portal with create, read, update and delete (CRUD) tools for every part of society operations, backed by a relational database with optimized queries.

The project was built for the **Software Design and Analysis** course at FAST University.

## Key Features

### For Students
- Account signup and login with email and password
- Browse the list of student societies and their details
- View competition details and register as a participant
- Register as an attendee for society events

### For Administrators
- **Admin portal dashboard** showing live totals for societies, events, participants and teams, queried from the database on every load
- **Societies**: add, edit and delete societies
- **Events**: schedule and manage events for each society
- **Competitions**: create competitions with fees and manage them
- **Participants**: view, add, edit and remove competition participants
- **Attendees**: manage event attendee lists
- **Team members**: manage society team rosters with positions and departments

### Security
- Passwords hashed with **bcrypt**
- Session-based authentication
- Role-based access control (`admin` and student roles)
- Admin signup restricted to an **approved admin email list**
- Server-side validation for signup (email format, duplicate email and username checks)

## Tech Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js |
| Web framework | Express |
| Templating | EJS |
| Database | MySQL |
| ORM / queries | Sequelize (with raw SQL queries in places) |
| Authentication | Passport (local strategy), express-session, bcrypt / bcryptjs |
| Front end | Bootstrap 5, Font Awesome |

## Development Approach

SocioStruct follows a design-first process: requirements and a domain model (class design) were produced before implementation, then built out feature by feature (authentication, societies, events, competitions, participants, team members, admin portal).

## System Design

The domain model was designed first and is included in the repository as Java class stubs (`Entity`, `Person`, `Admin`, `society`, `event`, `competiton`, `teammember`, and others).

```
Entity (abstract)                Person (abstract)
├── society                      ├── Admin
├── event                        ├── teammember
└── competiton                   ├── eventattendee
                                 └── Competitionparticipants

society  1 ── *  event  1 ── *  competiton  1 ── *  Competitionparticipants
society  1 ── *  teammember
event    1 ── *  eventattendee
```

The web application follows an MVC-style structure: Express routes and controllers expose HTTP endpoints for each resource, Sequelize models and SQL queries talk to the relational database, and EJS templates render the views.

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) 18 or later
- [MySQL](https://www.mysql.com/) 8 or later
- npm

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/aliansari07/SocioStruct.git
   cd SocioStruct
   ```

2. **Install dependencies**
   ```bash
   npm install express ejs sequelize mysql2 express-session passport passport-local bcryptjs
   ```

3. **Create the database**
   ```sql
   CREATE DATABASE sociostruct;
   ```

4. **Configure the database connection**

   Update your database configuration file with your MySQL host, user, password and database name. Keep credentials out of version control, for example by using a `.env` file.

5. **Seed the admin email list**

   Admin accounts can only be created with an email listed in the `AdminEmail` table. Insert the email addresses you want to authorize before signing up as an admin.

6. **Start the server**
   ```bash
   node app.js
   ```

   Then open `http://localhost:3000` in your browser.

> **Note:** Adjust the entry file name, port and configuration steps above to match your local setup.

## Usage

1. Go to `/signup` and create an account. Choose the **admin** role only if your email is on the approved list.
2. Log in at `/login`.
3. Students can browse societies, competitions and events and register.
4. Admins are taken to the **Admin Portal**, where they can manage societies, events, competitions, participants, attendees and team members.

## Route Overview

| Area | Examples |
|---|---|
| Authentication | `GET/POST /signup`, `GET/POST /login`, `GET /logout` |
| Dashboard | `GET /` |
| Societies | `/societies`, `/societies/add`, `/societies/edit/:id`, `/societies/delete/:id` |
| Events | `/events`, `/events/add`, `/events/edit/:id`, `/events/delete/:event_id` |
| Competitions | `/competitions`, `/competitions/add`, `/competitions/edit/:id`, `/competitions/delete/:id` |
| Participants | `/participants`, `/participants/delete/:id` |
| Attendees | `/attendees`, `/attendees/delete/:attendee_id` |
| Team members | `/members`, `/members/add`, `/members/:id/edit`, `/members/delete/:id` |
| Admin portal | `/admin`, `/admin/societies`, `/admin/events`, `/admin/participants`, `/admin/teams` |

## Roadmap

- [ ] Consolidate the project into a clean folder structure (`routes/`, `controllers/`, `models/`, `views/`)
- [ ] Add a `package.json` and `.env.example`
- [ ] Switch destructive actions from `GET` to `POST`/`DELETE` routes
- [ ] Add input validation and flash messages across all forms
- [ ] Add automated tests
- [ ] Email notifications for event registration
- [ ] Deploy a hosted demo

## Contributing

Contributions are welcome.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m "Add your feature"`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a pull request

## Authors

- **Muhammad Ali Ansari**: [@aliansari07](https://github.com/aliansari07)

---

<div align="center">

Built for the Software Design and Analysis course at FAST University.

</div>
