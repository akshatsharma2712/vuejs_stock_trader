<template>
   <div   class="col-sm-6 col-md-4" style="margin-top:15px;" >
        <div class="card">
            <div class="card-header bg-info text-white">
                <h3 class="card-title">{{stock.name}}
                    <small>(Price: {{stock.price}} | Quantity: {{stock.quantity}})</small>
                </h3>
            </div>
            <div class="card-body">
                <div class="float-left">
                    <input type="number" class="form-control" placeholder="quantity" v-model.number="quantity">
                </div>
                <div class="float-right">
                    <button class="btn btn-danger" 
                    @click="sellStock"
                    :disabled="insufficientQuantity || quantity<=0|| (!Number.isInteger(quantity))" > 
                        {{insufficientQuantity?'Unable':'Sell'}}</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import {mapActions} from 'vuex';
export default {
    props:['stock'],
    data()
    {
        return {
            quantity:0
        }    
    },
    computed:{
        insufficientQuantity()
        {
             return this.quantity> this.stock.quantity;
        }
    },
    methods:{
        ...mapActions({
            placeSellOrder: 'sellStock'
        }),
        sellStock()
        {
            const order= {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity
            };
            this.placeSellOrder(order);//in the store
            this.quantity =0;
        }
    }
};
</script>