<template>
  <div v-if="show" id="modal" class="modal is-active">
    <div class="modal-background"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">Edit: {{column}}</p>
        <button class="delete" aria-label="close" v-on:click="$emit('toggleModal')"></button>
      </header>
      <div class="modal-card-body">
        <div class="box">
          <article class="media">
            <div class="media-content">
              <div class="content">
                <input class="input" type="text" v-model="newColumnName" placeholder="New Column Name">
              </div>
            </div>
          </article>
        </div>
      </div>
      <footer class="modal-card-foot">
        <button class="button is-success" v-on:click="updateColumn(newColumnName)">Save changes</button>
        <button class="button" v-on:click="$emit('toggleModal')">Cancel</button>
      </footer>
    </div>
    <button class="modal-close is-large" aria-label="close" v-on:click="$emit('toggleModal')"></button>
  </div>
</template>

<script>
export default {
  name: 'ModalEdit',
    props: ['show', 'column']
  ,
  data: function() {
    return {
      newColumnName: "",
      addableHeaders: ['firstname', 'surname', 'address1', 'town', 'postcode']
    };
  },
  methods: {
    updateColumn(newColumnName) {
      this.$emit('modifyData', newColumnName);
      this.newColumnName = "";
    }
  }
}
</script>



<!-- 

TDO


 -->
