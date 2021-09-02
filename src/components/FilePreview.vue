<template>
  <div class="preview">
    <!-- <p>{{fileData}}</p> -->
    <table class="table table-bordered">
      <thead>
        <tr>
          <th v-for="(value, name, index) in fileData[0]" :key="name">{{name}} 
            <i v-on:click="toggle(name)" class="bi-pen"></i>
            <i v-on:click="deleteColumn(name, index)" class="bi-trash"></i>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, index) in fileData" :key="index">
          <td v-for="(col, index) in row" :key="index">{{col}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>


export default {
  name: 'FilePreview',
  props: {
    fileData: {}
  },
  methods: {
    toggle (name) {
      this.$emit('toggleModal', name);
    },
    deleteColumn (name) {
      if (confirm("Are you sure you want to remove column " + name + "?")) {
        const modifiedData = this.fileData;
        modifiedData.forEach(function(row) {
          delete row[name];
        })
        this.$emit('modifyData', modifiedData);
      }
    }
  }
}
</script>


<!-- 

TDO

  Edit Headers

 -->