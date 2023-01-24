<template>
    <div class="card" style="width: 18rem;">
                    <img :src="`${store.imagBasePath}${product.cover_image}`" class="card-img-top" :alt="product.name">
                    <div class="card-body">
                        <h5 class="card-title">{{product.name}}</h5>
                        <p class="card-text">{{ truncateContent }}</p>
                        <router-link class="btn btn-primary" :to="{name: 'product', params:{slug: product.slug}}">
                        Vedi il prodotto
                        </router-link>                    
                    </div>
                </div>
</template>

<script>
import {store} from '../store';
    export default {
        name: 'ProductCard',
        props: ['product'],
        data(){
            return {
                store,
                contentMaxLen: 100
            }
        },
        computed:{
            truncateContent(){
                if(this.product.description.length > this.contentMaxLen){
                    return this.product.description.substr(0,this.contentMaxLen) + '...';
                }
                return this.product.description;            
            }
        }
        
    }
</script>

<style lang="scss" scoped>
</style>