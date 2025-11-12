
>This file helps Gemini understand the project's context, conventions, and goals.

  

## 1. Project Overview

- **Project Name:** Grace Land Nexus

- **Description:** A web application for a real estate business specializing in land sales. It provides listings, company information, and a contact portal for clients. The project also includes an admin dashboard for managing properties, inquiries, and website content.

- **Primary Goal:** To serve as the main online presence for Grace Properties, attracting new clients and streamlining the initial inquiry process.

  

## 2. Key Technologies

  

- **Frontend:** React, Vite, TypeScript

- **UI Framework:** shadcn-ui

- **Styling:** Tailwind CSS

- **Routing:** React Router

- **Animations:** GSAP

- **State Management:** React Query (TanStack Query)

- **Linting:** ESLint

  

## 3. Development Commands

  

- **Install Dependencies:** `npm install`

- **Start Development Server:** `npm run dev`

- **Build for Production:** `npm run build`

- **Lint Code:** `npm run lint`

  

## 4. Coding Style & Conventions

  

- **Component Structure:** Functional components with React Hooks.

- **Styling:** Utility-first classes with Tailwind CSS. Custom styles are minimal and located in `src/index.css`.

- **File Naming:** PascalCase for component files (e.g., `MyComponent.tsx`).

- **State Management:** Use React Query for server state and `useState`/`useReducer` for local UI state.

- **API Calls:** Use `fetch` or a library like `axios` for API interactions. (Note: Currently, the project uses mock data).

  

## 5. Future Goals / Roadmap

  

- **Migration to Next.js:** The user has expressed interest in migrating the frontend to Next.js to leverage SSR/SSG and improve performance.

- **Spring Boot Backend:** The long-term plan includes developing a dedicated backend using Spring Boot to replace the current mock data and provide a full-fledged REST API.

- **Authentication:** Implement a robust authentication system for the admin dashboard.

- **Database Integration:** Connect the application to a relational database (e.g., PostgreSQL) via the Spring Boot backend.