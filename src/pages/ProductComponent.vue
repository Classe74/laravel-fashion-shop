<template>
    <section v-if="product">
    <h1>{{ product.name }}</h1>
    <img :src="`${store.imagBasePath}${product.cover_image}`" class="card-img-top" :alt="product.name">
    <p>{{ product.description }}</p>
    <div v-if="post.category">
     <h5>Category: {{ product.category.name }}</h5>
    </div>
    <div v-if="product.tags && product.tags.length > 0">
     <h5>Tags</h5>
     <div>
         <span v-for="(tag,index) in product.tags" :key="index" class="badge text-bg-info">{{ tag.name }}</span>
     </div>
    </div>
    </section>
    <section v-else>Loading...</section>
 </template>
 
 <script>
     import axios from 'axios';
     import { store } from '../store';
     export default {
         name: 'ProductComponent',
         data(){
             return {
                 store,
                 product: null,
             }
         },
         methods:{
             getProduct(){
                 console.log(this.$route);
                  axios.get(`${this.store.apiBaseUrl}/products/${this.$route.params.slug}`).then((response)=>{
                     //console.log(response.data.results);
                     if(response.data.success){
                         //console.log(response.data.results);
                         this.product = response.data.results;
                     } else {
                         //console.log(this.$router);
                         this.$router.push({name: 'not-found'});
                     }
                    
                 });         
             }
         },
         mounted(){
         //     this.$watch(() => this.$route.params, (toParams, previousParams) => {
         //  if(toParams !== previousParams){
             this.getProduct();
         //      }
         //   }
         // )
   },
             
         }
         
 </script>
 
 <style lang="scss" scoped>
 </style>
 