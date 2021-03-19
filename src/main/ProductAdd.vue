<template>
    <div>
        <center>
        <h1 class="text-warning">Crud Operation</h1><br />
        <form>
            <input disabled hidden type="text" v-model="prdocutlist.id"  @change="$emit('update:id', $event.target.value)"  placeholder="automatic assign">
            Name: <input type="text" v-model="prdocutlist.name"  @change="$emit('update:name', $event.target.value)" > &nbsp;&nbsp;
            Category: <input type="text" v-model="prdocutlist.category"  @change="$emit('update:category', $event.target.value)">&nbsp;&nbsp;
            Price: <input type="text" v-model="prdocutlist.price" @change="$emit('update:price', $event.target.value)">&nbsp;&nbsp;
            Qty: <input type="text" v-model="prdocutlist.qty" @change="$emit('update:qty', $event.target.value)" ><br /><br/>
            Total: <input type="text" v-model="prdocutlist.total" @change="$emit('update:total', $event.target.value)" >&nbsp;&nbsp;
            Status: <input type="text" v-model="prdocutlist.status" @change="$emit('update:status', $event.target.value)">&nbsp;&nbsp;
            Rating: <input type="text" v-model="prdocutlist.rating" @change="$emit('update:rating', $event.target.value)" ><br /><br/>
            
        <h1 class="text-warning">Product Variants</h1><br />
        <div v-for="(product,index) in prdocutlist.products" :key='index'>
            <!-- id:  <input type="text" :value="child_id"  @change="$emit('update:child_id', $event.target.value)"  placeholder="Add id to add Item in place"><br/><br/> -->
            Name: <input type="text" v-model="product.prod_name"  @change="$emit('update:prod_name', $event.target.value)" > &nbsp;&nbsp;
            Color: <input type="text" v-model="product.color"  @change="$emit('update:color', $event.target.value)">&nbsp;&nbsp;
            Size: <input type="text" v-model="product.size" @change="$emit('update:size', $event.target.value)">&nbsp;&nbsp;
            Product Price: <input type="text" v-model="product.prod_price" @change="$emit('update:prod_price', $event.target.value)" >&nbsp;&nbsp;
            <button class="btn-danger" @click="removethis(index)">- Remove</button><br /><br/>
            
            <!-- <button class="btn-primary" @click="addprod(child_id)">Add Product Varient</button>&nbsp;&nbsp;
            <button class="btn-success" @click="updateProd(id,child_id)">Update Product Varient</button><br /><br/> -->
            
            <!--  -->
        </div>
        <button class="btn-success" @click="addmore">+ Add More</button><br /><br/>
        <!-- <button class="btn-success" @click="update(id)">Update</button> -->
        <button class="btn-primary" @click="add">Add Product</button><br /><br/>
        </form>
        </center>
    </div>
</template>
<script>
export default {
    name:'ProductAdd',
    props:{
        Product_Data:Object,
        currIndex:Number
    },
    watch:{
        currIndex:function(newVal){
            // console.log(newVal)
            if(newVal>-1){
                this.updatevalue()
            }
        }
    },
    data(){
        return{
            prdocutlist:
                {
                    name:'',
                    category:'',
                    price: '',
                    qty: '',
                    total: '',
                    status: '',
                    rating:'', 
                    products:[{
                        prod_name:'',
                        color:'',
                        size:'',
                        prod_price:''
                    }]
                },
                variants:{
                        prod_name:'',
                        color:'',
                        size:'',
                        prod_price:''
                    }
            
        }
    },
    methods:{
        defaultprod(){
            return{
                prod_name:'',
                color:'',
                size:'',
                prod_price:''
            }
        },
        default(){
            return{
                name:'',
                category:'',
                price: '',
                qty: '',
                total: '',
                status: '',
                rating:'', 
                products:[{
                        prod_name:'',
                        color:'',
                        size:'',
                        prod_price:''
                    }]
            }
        },
        add(){
            console.log(this.currIndex)
            if(this.currIndex >-1){
                this.$emit('updateItem',{index: this.currIndex,form: this.prdocutlist})
                this.prdocutlist = this.default()
                console.log(this.currIndex)
            }
            else{
                 this.$emit('additem',this.prdocutlist)
                this.prdocutlist = this.default()
                console.log(this.currIndex)
            }
        }, 
        addmore(){
            this.prdocutlist.products.push(this.variants)
            this.variants = this.defaultprod()
        },
        removethis(index){
            this.prdocutlist.products.splice(index, 1);
        },
        updatevalue(){
            console.log(this.Product_Data)
            this.prdocutlist=this.Product_Data
        }
    }
}
</script>