<template>
    <section>
    <h1>Lista dei prodotti</h1>
    <div class="row">
            <div class="col-12 col-md-4" v-for="(product, index) in products" :key="product.id">
                <ProductCard :product="product" />
            </div>
    </div>
    <nav aria-label="Page navigation example">
  <ul class="pagination">
    <li class="page-item" :class="{'disabled': currentPage === 1}">
        <button class="page-link" :disabled="currentPage === 1" @click="getProducts(currentPage - 1)">Previous
        </button>
    </li>
    <li class="page-item" v-for="n in lastPage">
        <button class="page-link" @click="getPosts(n)">{{n}}</button>
    </li> 
    <li class="page-item" :class="{'disabled': currentPage === lastPage}">
        <button class="page-link" :disabled="currentPage === lastPage" @click="getProducts(currentPage + 1)">Next
        </button>
    </li>   
  </ul>
</nav>
    </section>
</template>

<script>
    import axios from 'axios';
    import { store } from '../store';
    import ProductCard from '../components/ProductCard.vue';
    export default {
        name: 'ProductList',
        components: {
            ProductCard
        },
        data(){
            return {
                store,
                products: [],
                currentPage: 1,
                lastPage: null,
                total: 0                
            }
        },
        methods:{
            getProducts(pagenum){
                axios.get(`${this.store.apiBaseUrl}/products`,{params:{
                   page: pagenum 
                }}).then((response)=>{
                    //console.log(response.data.results);
                   this.products = response.data.results.data;
                   this.currentPage = response.data.results.current_page;
                   this.lastPage = response.data.results.last_page;
                   this.total = response.data.results.total;
                })
            }           
        },
        mounted(){
            this.getProducts(1);
        }
    }
</script>

<style lang="scss" scoped>
</style>