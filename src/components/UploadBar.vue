<template>
  <div class="upload">
    <div class="input-group mb-3">
      <input type="file" aria-label="Upload" accept=".csv" @change="validateFile">
    </div>
    <span v-if="error">Wrong Filetype</span>
  </div>
</template>

<script>
export default {
  name: 'UploadBar',
  data: function() {
    return {
      error: 0
    };
  },
  methods: {
    validateFile (e) {
      this.error = 0;
      let file = e.target.files[0];
      file.type == "application/vnd.ms-excel" ? this.createPreviewData(file) : this.error = 1;
    },
    createPreviewData (file) {
      const reader = new FileReader();
      reader.readAsText(file);
      const result = [];
      reader.onload = () => {
        const text = reader.result;
        let lines = [];
        const linesArray = text.split('\n');
        linesArray.forEach((e) => {
            const row = e.replace(/[\s]+[,]+|[,]+[\s]+/g, ',').trim();
            lines.push(row);
        });
        lines.splice(lines.length - 1, 1);
        const headers = lines[0].split(",");
        for (let i = 1; i < lines.length; i++) {
          const obj = {};
          const currentline = lines[i].split(",");
          for (let j = 0; j < headers.length; j++) {
            obj[headers[j]] = currentline[j];
          }
          result.push(obj);
        }
      }
      this.$emit('passData', result);
    }
  }
}
</script>



<!-- 

TDO

  More Validation
    FileSize

 -->
