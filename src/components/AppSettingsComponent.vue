<script type="text/javascript">

</script><template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">Settings</h5>
      <button @click="exportTasks" class="btn btn-outline-info me-2">Export Tasks</button>
      <input type="file" @change="importTasks" class="form-control d-inline-block w-auto" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppSettingsComponent',
  methods: {
    exportTasks() {
      this.$emit('export-tasks');
    },
    importTasks(event) {
      this.$emit('import-tasks', event);
    }
  }
};
</script>