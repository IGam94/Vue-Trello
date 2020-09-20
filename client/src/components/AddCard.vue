<template>
  <div class="add-card">
    <form @submit.prevent="onSubmit">
      <input type="text" class="form-control" v-model="inputTitle" ref="inputText">
      <button class="btn-success btn" type="submit" :disabled="invalidInput">카드 생성</button>
      <a href="" class="cancel-add-btn" @click.prevent="$emit('close')">&times;</a>
    </form>

  </div>
</template>

<script>
import {mapActions} from 'vuex'
  export default {
    props:['listId'],
    data(){
      return {
        inputTitle:''
      }
    },
    computed: {
      invalidInput(){
        return !this.inputTitle.trim()
      }
    },
    mounted() {
      this.$refs.inputText.focus()
      this.setupClickOutside(this.$el)
    },
    methods: {
      ...mapActions([
        'ADD_CARD'
      ]),
      onSubmit(){
        if (this.invalidInput) return 
        const {inputTitle,  listId} = this
        this.ADD_CARD({title: inputTitle,  listId})
        .finally(() => this.inputTitle = '')
        
      },
      
    },
  }
</script>

<style>
.form-control {
  background-color: white;
}
.add-card {
  padding: 10px;
  display: block;
  position: relative;
}
.add-card .cancel-add-btn {
  display: inline-block;
  margin-left: 10px;
  vertical-align: middle;
  text-decoration: none;
  color: #888;
  font-size: 24px;
}
.add-card .cancel-add-btn:hover,
.add-card .cancel-add-btn:focus {
  color: #666;
}
</style>