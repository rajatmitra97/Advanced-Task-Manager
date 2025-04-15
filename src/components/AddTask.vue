<script type="text/javascript">

    </script><template>
  <div class="card mb-4">
    <div class="card-body">
      <h5 class="card-title">Add New Task</h5>
      <div class="row g-2">
        <div class="col-md-4">
          <input v-model="newTaskTitle" class="form-control" placeholder="Task title" />
        </div>
        <div class="col-md-3">
          <select v-model="newTaskCategory" class="form-select">
            <option value="">Select Category</option>
            <option v-for="cat in categories" :key="cat" :value="cat">{{ cat }}</option>
          </select>
        </div>
        <div class="col-md-3">
          <input type="date" v-model="newTaskDueDate" class="form-control" />
        </div>
        <div class="col-md-2">
          <button @click="addTask" class="btn btn-primary w-100">Add Task</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['categories'],
  data() {
    return {
      newTaskTitle: '',
      newTaskCategory: '',
      newTaskDueDate: ''
    };
  },
  methods: {
    addTask() {
      if (!this.newTaskTitle.trim()) return;
      const newTask = {
        id: Date.now(),
        title: this.newTaskTitle.trim(),
        category: this.newTaskCategory || '',
        dueDate: this.newTaskDueDate || '',
        completed: false,
        priority: 'medium',
        isEditing: false,
        editedTitle: ''
      };
      this.$emit('add-task', newTask);
      this.newTaskTitle = '';
      this.newTaskCategory = '';
      this.newTaskDueDate = '';
    }
  }
};
</script>