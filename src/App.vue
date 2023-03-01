<template>
  <div class="container column">

    <block-constructor-form></block-constructor-form>

    <div class="card card-w70" v-if="!loading">
      <button v-if="blocks.length" class="btn primary" @click.prevent="deleteAllBlocks">Очистить резюме</button>
      <component  v-if="blocks.length"  v-for="block in blocks" :is="'block-'+block.type" :block="block"></component>
      <block-h3 v-else :block="{content:'Добавьте первый блок, чтобы увидеть результат'}"></block-h3>
    </div>

    <div class="card card-w70" v-else><loader ></loader></div>
  </div>

  <comments></comments>

</template>

<script>
import {defineAsyncComponent} from "vue";
import BlockConstructorForm from "@/components/BlockConstructorForm";
import Comments from "@/components/Comments";
import axios from "axios";
import Loader from "@/components/Loader";

export default {
  components:{
    Loader,
    BlockConstructorForm,
    Comments,
    BlockH1:defineAsyncComponent(()=>import('@/components/Blocks/BlockH1')),
    BlockH2:defineAsyncComponent(()=>import('@/components/Blocks/BlockH2')),
    BlockH3:defineAsyncComponent(()=>import('@/components/Blocks/BlockH3')),
    BlockAvatar:defineAsyncComponent(()=>import('@/components/Blocks/BlockAvatar')),
    BlockP:defineAsyncComponent(()=>import('@/components/Blocks/BlockP')),
  },

  data(){return{
    blocks:[],
    loading:false
  }},
  provide() {
    return {
      blocks: this.blocks
    }
  },

  mounted() {
    this.loadBlocks()
  },

  methods:{
    async loadBlocks(){
      this.loading = true
      try {
        const {data} = await axios.get('https://resumeconstructor-b3333-default-rtdb.firebaseio.com/blocks.json')

        this.blocks.push(...Object.keys(data).map(key=>{
          return{
            id:key,
            ...data[key]
          }
        }))
      }catch (e){

      }
      this.loading = false
    },
    async deleteAllBlocks(){
      this.blocks.forEach( e=>{
        this.deleteBlock(e.id)
      })
    },


    async deleteBlock(id){
      this.loading = true
      await axios.delete(`https://resumeconstructor-b3333-default-rtdb.firebaseio.com/blocks/${id}.json`)
          .then(res=>{
            this.blocks = this.blocks.filter(block=>block.id !== id)
          })
          .catch(err=>{

          })

      this.loading = false
    }
  }

}
</script>

<style>

</style>
