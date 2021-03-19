<template>
<div>
    <ProductAdd :Product_Data="updated_products" :currIndex="currentIndex" @addMore="addmore" @additem="add" @updateItem="update"/>
    <ProductList :prods='prods' :columns='columns' @removeitem="remove" @removechilditem="removeChild" @edititem="edit"/>
</div>
</template>
<script>
import ProductList from './main/ProductList'
import ProductAdd from './main/ProductAdd'
export default {
  name: 'App',
  components: {
    ProductAdd,
    ProductList
  },
  data(){
    return{
        currentIndex:-1,
        columns:['Index','Name','Category','Price','Qty','Total','Status','Rating','Product Variants','Actions'],
        prods: [
          {
              name: 'MI',
              category: 'TV',
              price: '15000',
              qty: '1',
              total: '15000',
              status: false,
              rating:'5',
              editable: false,
              products:[
                {
                  prod_name:'MI Note 5 pro',
                  color:'Black',
                  size:'6.5 inch',
                  prod_price:'15000',
                  editable: false
                }
              ]
          },
        ],
        updated_products:{
          
        },
    }
  },
  methods:{
        edit(p,index){
          this.currentIndex=index
          this.updated_products=p
        },
        remove(index){
            this.prods.splice(index, 1);
        },
        removeChild(index,child_index){
          this.prods[index].products.splice(child_index,1);
        },
        add(e){
          this.prods.push(e);
        },
        update(p){
          this.prods[p.index] = p.form;
          this.currentIndex = -1
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
