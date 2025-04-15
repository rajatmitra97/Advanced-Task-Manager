<script type="text/javascript">

    </script><template>
  <div class="btn-group mb-3">
    <button @click="setFilter('all')" class="btn btn-outline-primary">All</button>
    <button @click="setFilter('completed')" class="btn btn-outline-primary">Completed</button>
    <button @click="setFilter('pending')" class="btn btn-outline-primary">Pending</button>
  </div>
</template>

<script>
export default {
  methods: {
    setFilter(filter) {
      this.$emit('set-filter', filter);
    }
  }
};
</script>