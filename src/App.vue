<template>
  <div id="app" class="app-container">
    <h1 class="text-center mb-3 fw-bold text-primary" style="font-family: 'Sans-serif', helvetica; letter-spacing: 0.5px;">
      <span class="d-inline-flex align-items-center bg-white px-3 py-1 rounded-3 shadow-sm border border-light">Advanced Task Manager</span></h1>
    <h2 class="text-center mb-2 fw-oblique text" style="font-family: 'Serif', garamond; letter-spacing: 1px;">
      <span class="d-inline-flex align-items-center bg-light px-2 py-1 rounded-pill shadow-sm">Rajat Raja</span></h2>
    <div class="container">
    <AddTask :categories="categories" @add-task="addTask" />
    <TaskFilter @set-filter="setFilter" />
    <div class="row mb-3">
      <div class="col-md-6">
        <input v-model="searchQuery" class="form-control" placeholder="Search tasks..." />
      </div>
      <div class="col-md-6">
        <select v-model="sortOption" class="form-select">
          <option value="title">Sort by Title</option>
          <option value="dueDate">Sort by Due Date</option>
          <option value="priority">Sort by Priority</option>
        </select>
      </div>
    </div>
    <TaskList :tasks="displayedTasks" @delete-task="deleteTask" @save-tasks="saveTasks" />
    <TaskSummary :tasks="tasks" />
    <CategoryManager :categories="categories" @add-category="addCategory" @delete-category="deleteCategory" />
    <Settings @export-tasks="exportTasks" @import-tasks="importTasks" />
    <DogPhoto />
    </div>
  
  </div>
</template>

<script>
import AddTask from './components/AddTask.vue';
import TaskFilter from './components/TaskFilter.vue';
import TaskList from './components/TaskList.vue';
import TaskSummary from './components/TaskSummary.vue';
import CategoryManager from './components/CategoryManager.vue';
import Settings from './components/AppSettingsComponent.vue';
import DogPhoto from './components/DogPhoto.vue'; 

export default {
  components: {
    AddTask,
    TaskFilter,
    TaskList,
    TaskSummary,
    CategoryManager,
    Settings,
    DogPhoto
  },
  data() {
    return {
      tasks: [],
      nextId: 1,
      filter: 'all',
      searchQuery: '',
      sortOption: 'title',
      categories: ['Work', 'Personal']
    };
  },
  computed: {
    filteredTasks() {
      if (this.filter === 'completed') {
        return this.tasks.filter(task => task.completed);
      } else if (this.filter === 'pending') {
        return this.tasks.filter(task => !task.completed);
      }
      return this.tasks;
    },
    searchedTasks() {
      if (!this.searchQuery) return this.filteredTasks;
      return this.filteredTasks.filter(task =>
        task.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
    displayedTasks() {
      const tasks = [...this.searchedTasks];
      if (this.sortOption === 'title') {
        return tasks.sort((a, b) => a.title.localeCompare(b.title));
      } else if (this.sortOption === 'dueDate') {
        return tasks.sort((a, b) => (a.dueDate || '').localeCompare(b.dueDate || ''));
      } else if (this.sortOption === 'priority') {
        const priorityOrder = { high: 3, medium: 2, low: 1 };
        return tasks.sort((a, b) => priorityOrder[b.priority] - priorityOrder[a.priority]);
      }
      return tasks;
    }
  },
  methods: {
    addTask(newTask) {
      newTask.id = this.nextId++;
      this.tasks.push(newTask);
      this.saveTasks();
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
      this.saveTasks();
    },
    setFilter(filter) {
      this.filter = filter;
    },
    saveTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    loadTasks() {
      const storedTasks = localStorage.getItem('tasks');
      if (storedTasks) {
        this.tasks = JSON.parse(storedTasks);
        this.nextId = Math.max(...this.tasks.map(t => t.id)) + 1 || 1;
      }
    },
    addCategory(category) {
      this.categories.push(category);
    },
    deleteCategory(category) {
      this.categories = this.categories.filter(cat => cat !== category);
      this.tasks = this.tasks.map(task => {
        if (task.category === category) task.category = '';
        return task;
      });
      this.saveTasks();
    },
    exportTasks() {
      const dataStr = JSON.stringify(this.tasks);
      const blob = new Blob([dataStr], { type: 'application/json' });
      const url = URL.createObjectURL(blob);
      const link = document.createElement('a');
      link.href = url;
      link.download = 'tasks.json';
      link.click();
      URL.revokeObjectURL(url);
    },
    importTasks(event) {
      const file = event.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = (e) => {
        try {
          const importedTasks = JSON.parse(e.target.result);
          this.tasks = importedTasks;
          this.nextId = Math.max(...this.tasks.map(t => t.id)) + 1 || 1;
          this.saveTasks();
        } catch (error) {
          alert('Invalid file format');
        }
      };
      reader.readAsText(file);
    }
  },
  mounted() {
    this.loadTasks();
  }
};
</script>

<style scoped>
.app-container {
  background-image: url('/src/assets/background.jpg');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
  min-height: 100vh; 
  position: relative;
}


.app-container::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(255, 255, 255, 0.5); 
  z-index: 1;
}


.app-container > * {
  position: relative;
  z-index: 2;
}


.container {
  background-color: rgba(255, 255, 255, 0.8); 
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); 
}
</style>