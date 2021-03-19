<template>
    <div>
        <center>
        <table class="table">
            <thead class="rounded thead-dark">
                <tr>
                <template v-for="(column,index) in columns">
                    <th :key='index'>{{column}}</th>
                </template>
                </tr>
            </thead>
            <tbody>
                <template v-for="(prod,index) in prods">
                <tr :key='index'>
                    <td>{{index+1}}</td>
                    <td>{{prod.name}}</td>
                    <td>{{prod.category}}</td>
                    <td>{{prod.price}}</td>
                    <td>{{prod.qty}}</td>
                    <td>{{prod.total}}</td>
                    <td>{{prod.status}}</td>
                    <td>{{prod.rating}}</td>
                    <td>
                        <table class="table">
                            <thead class="thead-dark">
                                <tr>
                                    <template>
                                        <th>id</th>
                                        <th>name</th>
                                        <th>color</th>
                                        <th>size</th>
                                        <th>price</th>
                                        <th>action</th>
                                    </template>
                                </tr>
                            </thead>
                            <tbody>
                                <template v-for="(prod_var,child_index) in prod.products">
                                    <tr :key="child_index">
                                        <td>{{child_index+1}}</td>
                                        <td>{{prod_var.prod_name}}</td>
                                        <td>{{prod_var.color}}</td>
                                        <td>{{prod_var.size}}</td>
                                        <td>{{prod_var.prod_price}}</td>
                                        <td style="width: 18%;">
                                            <!-- <a href="#" @click="editChild(index,child_index)" cla qss="btn btn-info">edit</a> -->
                                            <a href="#" class="btn btn-danger" @click="removeChild(index,child_index)">remove</a>
                                        </td>
                                    </tr>
                                </template>
                            </tbody>
                        </table>
                    </td>
                    <td style="width: 18%;">
                        <a href="#" @click="edit(prod,index)" class="btn btn-info">edit</a>
                        <a href="#" class="btn btn-danger" @click="remove(index)">remove</a>
                    </td>
                    
                </tr>
                </template>
            </tbody>
        </table>
        </center>
    </div>
</template>
<script>
export default {
    name:'ProductList',
    props:{
        prods :{type:Array},
        columns :{type:Array},
    },
    data(){
        return{
            // id:'',
            name: '',
            category: '',
            price: '',
            qty: '',
            total: '',
            status: '',
            rating:'',
        }
    },
    methods:{
        remove(index){
            this.$emit('removeitem',index)
        },
        edit(prods,index){
            this.$emit('edititem',prods,index)
        },
        removeChild(index, child_index){
            this.$emit('removechilditem',index,child_index)
        },
        // editChild(index,child_index){
        //     this.$emit('editchilditem',index,child_index)
        // }
    }
}
</script>