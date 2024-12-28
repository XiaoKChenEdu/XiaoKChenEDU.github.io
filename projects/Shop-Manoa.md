---
layout: project
type: project
image: img/projects/Shop-Manoa/uhLogo.png
title: "Shop-Manoa"
date: 2024
published: true
labels:
  - ICS 314 Final Project
  - Web Development
  - Meteor
  - React
  - MongoDB
  - Bootstrap 5
  - JavaScript
summary: "A web application designed to facilitate buying and selling of campus-related items within the UH Manoa community."
---

<img class="img-fluid" src="../img/projects/Shop-Manoa/Shop-Manoa.jpg">

## Overview
Shop-Manoa is a comprehensive marketplace web application developed as a final project for ICS 314. Built using Meteor and React, it serves as a dedicated platform where UH Manoa students, faculty, and staff can buy, sell, or trade campus-related items. The application promotes sustainability through the reuse and recycling of academic materials and student life essentials.

You can explore the project through these links:
- [Organization Page](https://shop-manoa.github.io/)
- [Source Code](https://github.com/shop-manoa/shop-manoa)

## System Architecture
```mermaid
graph TD
    A[Client Browser] -->|HTTP/WebSocket| B[Meteor Server]
    B -->|MongoDB Operations| C[(MongoDB Database)]
    B -->|Authentication| D[User Management]
    B -->|File Storage| E[Image Storage]
    
    subgraph Frontend
    F[React Components]
    G[Bootstrap UI]
    H[User Interface]
    end
    
    F -->|Renders| H
    G -->|Styles| H
    H -->|User Input| A
```

## User Flow Diagram
```mermaid
flowchart LR
    A[Start] --> B{Logged In?}
    B -->|No| C[Sign Up/Login]
    B -->|Yes| D[Browse Items]
    D --> E[View Item]
    E --> F{Buy or Sell?}
    F -->|Buy| G[Contact Seller]
    F -->|Sell| H[Create Listing]
    H --> I[Manage Items]
    G --> J[Complete Transaction]
    I --> K[End]
    J --> K
```

## Component Structure
```mermaid
classDiagram
    class App {
        +Router
        +NavBar
        +Footer
    }
    class UserProfile {
        +UserInfo
        +ListingsManager
    }
    class ItemList {
        +SearchBar
        +FilterSystem
        +ItemCards
    }
    class Authentication {
        +SignUp
        +SignIn
        +SignOut
    }
    App --> UserProfile
    App --> ItemList
    App --> Authentication
```

## Features
- User authentication and profile management
- Item listing with detailed descriptions and images
- Category-based browsing
- Search functionality
- Responsive design for mobile and desktop
- Real-time updates using Meteor's reactive data

## My Contributions
- Designed and implemented the Profile Page with user information display and editing capabilities
- Created the List Profile Page for managing user listings
- Enhanced the Item List Page with improved filtering and sorting features
- Optimized the Sign Up Page for better user experience
- Implemented responsive design principles across multiple pages
- Conducted code reviews and resolved merge conflicts
- Participated in milestone planning and documentation

## Technical Skills Applied
- Frontend Development: React, Bootstrap 5
- Backend Development: Meteor, MongoDB
- Version Control: Git, GitHub
- Project Management: Issue tracking, Milestone planning
- Testing: TestCafe

## What I Learned
Through this project, I gained valuable experience in:
- Full-stack web development using the Meteor framework
- Agile development methodologies and team collaboration
- Git workflow and merge conflict resolution
- UI/UX design principles and implementation
- Database design and management
- Deployment and hosting considerations
- Creating and maintaining technical documentation