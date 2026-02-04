# README

A light-weight, cross-platform desktop application to help users track job applications with minimal friction. Built using Rust, SQLite, and Tauri, this app is designed to replace spreadsheets with a faster, local-first tool.

## Motivation
During my job searches, I tracked job applications using apps like Google Sheets, but I found the workflow to be repetitive and clunky. I wanted something faster and more user friendly while also helping me keep track of my applications.

## Features (V1)
- Cross platform desktop application
- Basic CRUD operations on job applications
- Persistent local storage using SQLite
- Status tracking (Waiting for response, Interviewing, Rejected, etc.)
- Filtering, sorting, searching
- Simple import/export functionality
- Keyboard-friendly data-entry

## Architecture Overview
This app was made with local-first development in mind with the intention of integrating an external app interface eventually. 

flowchart TD
    UI[Frontend UI\n(Tables, Forms, Filters)]
    BE[Rust Backend\n(Tauri Commands, Validation, Command Handlers)]
    DB[(SQLite Database)]

    UI -->|invoke| BE
    BE -->|SQL queries| DB

## Data Model
### Application

Each job application is stored as a single record in SQLite.

| Field        | Type    | Description                 |
|--------------|---------|-----------------------------|
| id           | UUID    | unique identifier           |
| company      | string  | company name                |
| title        | string  | job title                   |
| location     | string  | job location                |
| pay          | integer | salary                      |
| status       | enum    | application status          |
| date_applied | date    | application submission date |
| last_heard   | date    | date of latest update       |
| job_url      | string  | link to job posting         |
| notes        | string  | additional notes or info    |
| resume       | UUID	 | resume used for job posting |

### Resume
Resumes are stored as separate entities and referenced by Applications

| Field | Type   | Description          |
|-------|--------|----------------------|
| id    | UUID   | unique identifier    |
| name  | string | resume name or label |
| path  | string | local file path      |

## Status Lifecycle
Statuses are editable and designed to support future analytics (e.g. response rates). This is a tentative list of supported statuses on a job application.

- Draft: unfinished entry
- Waiting for response: application is submitted and waiting for response
- Interviewing: currently undergoing interviewing for job posting
- Offer: received offer
- Negotiating: negotiating the terms of the role
- Rejected: self-rejected or company rejection of application
- Ghosted: no-response from recruiter
- Withdrawn: withdrawn an already completed application

## License
MIT

## Author
Built by Sergio Pantoja
