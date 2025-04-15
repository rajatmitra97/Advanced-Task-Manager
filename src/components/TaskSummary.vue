<script type="text/javascript">
    </script><template>
  <div class="dashboard mb-4">
    <h5>Task Summary</h5>
    <p>Total Tasks: {{ tasks.length }}</p>
    <p>Completed: {{ completedTasks }}</p>
    <p>Pending: {{ pendingTasks }}</p>
    <div class="progress">
      <div class="progress-bar" :style="{ width: completionPercentage + '%' }">
        {{ completionPercentage }}%
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['tasks'],
  computed: {
    completedTasks() {
      return this.tasks.filter(t => t.completed).length;
    },
    pendingTasks() {
      return this.tasks.filter(t => !t.completed).length;
    },
    completionPercentage() {
      if (this.tasks.length === 0) return 0;
      return Math.round((this.completedTasks / this.tasks.length) * 100);
    }
  }
};
</script>

<style scoped>
.dashboard { background-color: #f8f9fa; padding: 15px; border-radius: 5px; }
</style>