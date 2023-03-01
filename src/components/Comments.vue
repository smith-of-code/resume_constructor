<template>
  <div class="container">
    <p>
      <button class="btn primary" v-if="!isLoaded" @click="load">Загрузить комментарии</button>
    </p>
    <div class="card">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item" v-for="item in comments">
          <div>
            <p><strong>{{item.email}}</strong></p>
            <small>{{item.body}}</small>
          </div>
        </li>
      </ul>
    </div>

  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Comments",
  data(){return{
    isLoaded:false,
    comments:[]
  }},
  methods:{
   async load(){
      this.loading = true
      try {
        const {data} = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')

        this.comments.push(...data)
        this.isLoaded = true
      }catch (e){

      }
      this.loading = false
    }
  }

}
</script>

<style scoped>

</style>