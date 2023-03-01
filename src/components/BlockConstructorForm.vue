<template>

  <form class="card card-w30">
    <div class="form-control">
      <label for="type" >Тип блока</label>
      <select id="type" v-model="type">
        <option value="h1">Заголовок</option>
        <option value="h2">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="p">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea id="value" v-model="content" rows="3"></textarea>
    </div>

    <button v-if="!loading" :disabled="addButtonDisable" class="btn primary" @click.prevent="addBlock">Добавить</button>
    <loader v-else></loader>
  </form>
</template>

<script>
import axios from 'axios'
import Loader from "@/components/Loader";
export default {
  name:'BlockConstructorForm',
  components: {Loader},
  inject: ['blocks'],
  data(){return{
    type:'h1',
    content:'',
    loading:false
  }},
  methods:{
    async addBlock(){
      this.loading = true
      if (this.validator()){
      const block = {
        type:this.type,
        content:this.content,
       }
        await axios({
         url:'https://resumeconstructor-b3333-default-rtdb.firebaseio.com/blocks.json',
          method:'POST',
          headers:{
           'Content-Type':'application/json'
          },
          data:block
        }).then(res=>{
          this.blocks.push(block)

         this.setDefaultData()
        }).catch(err=>{

        })

      }
      this.loading = false
    },

    setDefaultData(){
      this.content = ''
      this.type = 'h1'
    },

    validator(){
      return this.content.length >= 3
    },
  },

  computed:{
    addButtonDisable(){
      return !this.validator()
    }
  },
}
</script>

<style scoped>
.loader{
  margin: 0 auto;
  width: 3em;
  height: 3em;
}

</style>