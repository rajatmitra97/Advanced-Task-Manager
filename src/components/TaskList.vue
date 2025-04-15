<script type="text/javascript">

    </script><template>
  <div class="card mb-4">
    <div class="card-body">
      <h5 class="card-title">Tasks</h5>
      <div v-for="task in tasks" :key="task.id" class="task-item d-flex align-items-center">
        <input type="checkbox" v-model="task.completed" @change="saveTasks" class="form-check-input me-2" />
        <span v-if="!task.isEditing" :class="{ completed: task.completed }" class="flex-grow-1">
          {{ task.title }} ({{ task.category || 'No Category' }}) - Due: {{ task.dueDate || 'N/A' }}
        </span>
        <input v-else v-model="task.editedTitle" class="form-control me-2" @keyup.enter="saveEdit(task)" />
        <select v-model="task.priority" @change="saveTasks" class="form-select me-2" style="width: 120px;">
          <option value="low">Low</option>
          <option value="medium">Medium</option>
          <option value="high">High</option>
        </select>
        <button v-if="!task.isEditing" @click="startEdit(task)" class="btn btn-sm btn-outline-secondary me-2">Edit</button>
        <button v-else @click="saveEdit(task)" class="btn btn-sm btn-outline-success me-2">Save</button>
        <button @click="deleteTask(task.id)" class="btn btn-sm btn-outline-danger">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['tasks'],
  methods: {
    startEdit(task) {
      task.isEditing = true;
      task.editedTitle = task.title;
    },
    saveEdit(task) {
      if (task.editedTitle.trim()) {
        task.title = task.editedTitle.trim();
        task.isEditing = false;
        this.$emit('save-tasks');
      }
    },
    deleteTask(id) {
      this.$emit('delete-task', id);
    },
    saveTasks() {
      this.$emit('save-tasks');
    }
  }
};
</script>

<style scoped>
.task-item { padding: 10px; border-bottom: 1px solid #ddd; }
.completed { text-decoration: line-through; color: gray; }
</style>