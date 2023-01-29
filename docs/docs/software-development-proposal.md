---
title: Software Development Proposal
layout: default
nav_order: 2
---

# Software Development Proposal
{: .no_toc }

Software Development Proposal for the Gregynog Management System project.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Introduction

### Motivation

Reduce the administration workload imposed on staff.

- It takes a lot of time to do the allocation
- Changes are difficult
- Reduce the number of emails exchanged between staff about changes

### Aims

The aim is to develop a web application to manage Gregynog events.

### Objectives

1. Collect requirements from all users where possible,
1. Design the overall architecture of the web application,
1. Implement a back-end for storing, processing and retrieving data,
1. Test the back-end implementation to ensure its correct functionality,
1. Implement a front-end to present the stored information to users, and
1. Test the front-end implementation to ensure its functionality.

### Deliverables

1. Web Application
1. Software Tests
1. Technical Reference Documentation
1. User Documentation

### Requirements

#### Core Requirements

##### Authentication and Authorization

1. Single sign-on (SSO) with Azure Active Directory
   1. This will allow students and staff to login with University accounts
1. Role-Based Access Control (RBAC)

   | Role               | Description         | Notes |
   |--------------------|---------------------|-------|
   | Organiser          | Event organisers    | |
   | Staff              | Lecturers           | |
   | Teaching Assistant | Marking support     | This role might not be needed |
   | Student            | Presenting projects | |

##### Logging

- All actions within the system must be logged for security purposes

##### Database

The database must store information about the following entities

1. User
   1. Staff
   1. Student
   1. Teaching Assistant
1. Cohort
1. Stream
1. Bedroom

##### User Interface

1. Input
   1. User can Create/Read/Update/Delete every database entity
   1. User can bulk-import data
1. Output
   1. User can view all database entities
      1. Students + all information entered by the student
         1. Dietary requirements (only visible to Organiser)
         1. Accessibility requirements (only visible to Organiser)
         1. Presentation adjustments (only visible to Staff/Teaching Assistant)
      1. Bedrooms
      1. Cohorts
      1. Streams

#### Additional Requirements

##### Forms

Allow students to enter information about their:

1. Projects
   - Name - e.g., Visualisation of geospatial data
   - Research area - AI/Security/Software Engineering/Computer Vision/...
1. Dietary requirements
1. Accessibility requirements

##### Allocation

The web application performs **semi-automatic allocations** based on the following requirements:

- Cohort
  - Soft Contraints
     1. Preferred cohort
     1. Supervisor is present
- Stream
  - Hard Contraints
     1. Maximum of 1 student per stream with presentation adjustments
     1. Student is not in the same stream as a first marker
  - Soft Contraints
      1. Projects are in a similar research area
      1. Student is not in the same stream as a second marker
- Bedroom
  - Allow group allocations
  - All students who want to live together must enter student numbers of all other students within the group

Note that some students might not go to Gregynog and should be therefore excluded from the allocation.

##### Emails

The system sends the following emails:

1. Reminderts to complete required forms
1. Notifications about changes

## Implementation

### Architecture

- Monolithic
- Layered
- Event-driven

### Technological Stack

The web application will be implemented using the following:

- C#
- ASP.NET Core
- EntityFramework Core
- MS-SQL server
- AutoMapper
- MediatR
- Ardalis.Specification
- FluentValidation

Tests will be implemented using the following NuGet packages (libraries):

- NUnit
- Moq
- FluentAssertions
- Respawn

### Design Patterns

- Repository
- CQRS
- Mediator
- Specification
