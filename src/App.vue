<template>
  <div id="app">
    <UploadBar @passData="updateData" />
    <FilePreview :fileData="previewData" @modifyData="updateData" @toggleModal="updateModal" />
    <ModalEdit :show="showModal" :column="editColumnName" @modifyData="renameColumn" @toggleModal="updateModal" />
  </div>
</template>

<script>


import UploadBar from './components/UploadBar.vue'
import FilePreview from './components/FilePreview.vue'
import ModalEdit from './components/ModalEdit.vue'

export default {
  name: 'App',
  components: {
    UploadBar,
    FilePreview,
    ModalEdit
  },
  data: function() {
    return {
      editColumnName: "",
      previewData: [],
      showModal: 0
    };
  },
  methods: {
    updateData (data) {
      this.previewData = [];
      this.$nextTick(function () {
        this.previewData = data;
      })
    },
    updateModal(newName) {
      this.showModal = !this.showModal;
      this.editColumnName = newName;
    },
    renameColumn(newName) {
      const modifiedData = this.previewData;
      const oldName = this.editColumnName;
      modifiedData.forEach(function(row) {
        row[newName] = row[oldName];
        delete row[oldName];
      })
      console.log("test");
      this.updateData(modifiedData);
      this.updateModal();
    },
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
