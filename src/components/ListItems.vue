<template>
  <div class="container">

    <!-- Button trigger modal -->
    <button type="button" class="btn btn-success float-end" data-bs-toggle="modal" data-bs-target="#exampleModal">
      Add +
    </button>

    <!-- Modal -->
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Add data</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <form>
              <div v-for="(key, index) in columns" :key="index" class="mb-3">
                <label class="form-label">{{ key }}</label>
                <input class="form-control">
              </div>
            </form>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
            <button type="button" class="btn btn-success">Save</button>
          </div>
        </div>
      </div>
    </div>

    <table v-if="data.length" class="table table-striped table-hover m-auto">
      <thead>
      <tr>
        <th v-for="(key, index) in columns" :key="index">{{ key }}</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(item, rowIndex) in data" :key="rowIndex">
        <td v-for="(key, colIndex) in columns" :key="colIndex">{{ item[key] }}</td>
      </tr>
      </tbody>
    </table>
    <p v-else>No data available.</p>

  </div>
</template>

<script>
export default {
  name:'ListItems',
  props: {
    data: {
      type: Array,
      required: true
    }
  },
  computed: {
    columns() {
      return this.data.length ? Object.keys(this.data[0]) : [];
    }
  }
};
</script>

<style scoped>
</style>
