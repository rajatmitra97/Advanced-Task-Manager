<script type="text/javascript">

    </script><template>
  <div class="card mb-4">
    <div class="card-body">
      <h5 class="card-title">Manage Categories</h5>
      <div class="input-group mb-2">
        <input v-model="newCategory" class="form-control" placeholder="New category" />
        <button @click="addCategory" class="btn btn-outline-success">Add</button>
      </div>
      <ul class="list-group">
        <li v-for="cat in categories" :key="cat" class="list-group-item d-flex justify-content-between">
          {{ cat }}
          <button @click="deleteCategory(cat)" class="btn btn-sm btn-outline-danger">Delete</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ['categories'],
  data() {
    return {
      newCategory: ''
    };
  },
  methods: {
    addCategory() {
      if (!this.newCategory.trim() || this.categories.includes(this.newCategory.trim())) return;
      this.$emit('add-category', this.newCategory.trim());
      this.newCategory = '';
    },
    deleteCategory(category) {
      this.$emit('delete-category', category);
    }
  }
};
</script>