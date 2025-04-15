# Task Manager

This is a Vue.js-based task manager app built to help organize your tasks efficiently. It’s packed with features to make task management straightforward and flexible, with a clean, modern interface powered by Bootstrap.

*A snapshot of the app, showing the sleek task list and intuitive controls.*

## Features

- **Add and Manage Tasks**: Create tasks with titles, categories, due dates, and priority levels (low, medium, high).
- **Edit and Delete**: Update task details or remove tasks as needed.
- **Filter and Search**: View all, completed, or pending tasks, and search by title for quick access.
- **Sort Tasks**: Organize tasks by title, due date, or priority to stay on top of what matters.
- **Categories**: Group tasks into custom categories like "Work" or "Personal" and manage them easily.
- **Task Summary**: Get a quick overview with total, completed, and pending task counts, plus a progress bar.
- **Export/Import Tasks**: Save tasks to a JSON file or load them back to keep your data portable.
- **Local Storage**: Tasks persist across browser sessions, so you don’t lose your work.

## Getting Started

### Prerequisites

- Node.js and npm installed.
- Vue CLI for development (`npm install -g @vue/cli`).

### Setup

1. Clone the repo:

   ```bash
   git clone <your-repo-url>
   cd task-manager
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Start the development server:

   ```bash
   npm run serve
   ```

4. Open `http://localhost:8080` in your browser to see the app.

### Project Structure

- `public/index.html`: Entry point for the app.
- `src/main.js`: Initializes Vue and Bootstrap.
- `src/App.vue`: Core component managing state and layout.
- `src/components/`: Includes `AddTask`, `TaskFilter`, `TaskList`, `TaskSummary`, `CategoryManager`, and `Settings` for modular functionality.

## Why I Built This

I wanted to create a practical tool that demonstrates Vue.js capabilities while keeping user experience in mind. This project showcases component-based design, state management, and useful features like task persistence and file handling, making it a solid example of modern web development.

## Future Ideas

- Add reminders for due dates.
- Support for task notes or subtasks.
- Integrate a backend for cloud storage.

Feel free to explore the code, try out the app, or suggest improvements!