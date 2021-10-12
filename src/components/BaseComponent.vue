<template>
  <div class="container">
    <h1>Data Dictionary</h1>
    <table class="table table-hover">
      <thead>
      <tr>
        <th scope="col">
          <select class="form-control">
            <option>Please select...</option>
          </select>
        </th>
        <th scope="col"></th>
        <th scope="col"></th>
        <th scope="col"></th>
        <th scope="col"></th>
        <th scope="col"></th>
      </tr>
      <tr>
        <th scope="col">ID</th>
        <th scope="col">Table</th>
        <th scope="col">Column</th>
        <th scope="col">Data Type</th>
        <th scope="col">Description</th>
        <th scope="col"></th>
      </tr>
      </thead>
      <tbody>
        <tr  v-for="row in rows" :key="row">
        <td> {{ row.id  }} </td>
        <td> {{ row.tableName }} </td>
        <td> {{ row.columnName }} </td>
        <td> {{ row.dataType }} </td>
        <td> {{ row.description }} </td>
        <td>
          <button v-on:click="update(row)" type="button" data-toggle="modal" data-target="#updateModal" class="btn btn-success btn-sm">Düzenle</button>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
  <!-- Modal -->
  <div class="modal fade" id="updateModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Update Description</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form>
            <div class="form-group">
              <label for="description">Description</label>
              <input type="text" class="form-control" id="description" aria-describedby="description" v-bind:value="currentRow.description">
            </div>
          </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
          <button type="button" class="btn btn-primary">Save changes</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
const axios = require('axios');

export default {
  data () {
    return {
      rows: [],
      currentRow:{},
    }
  },
  methods: {
    update: function (row) {
      this.currentRow = row
    }
  },
  mounted() {
    axios.get('http://localhost:8031/dictionary')
        .then(response => (this.rows = response.data))
        .catch(function (error) {
          console.log(error);
        })
        .finally(function (res) {
          console.log(res);
        })
  }
}
</script>