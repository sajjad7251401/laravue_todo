<template>
    <div class="add-item">
        <input type="text" v-model="item.name" v-on:itemadded="$emit(reloadlist)">
        <button :class="[ item.name ? 'active' : 'inactive', 'add-button']" @click="addItem()">Add</button>
    </div>
</template>

<script>
export default {
    data:function () {
        return {
            item:{
                name: ''
            }
        }
    },
    methods:{
        addItem(){
            if(this.item.name == ""){
                return false;
            }

            axios.post('api/item/store',{
                item: this.item
            }).then(response => {
                if(response.status == 201){
                    this.item.name = '';
                    this.$emit('itemchanged');
                }
            }).catch(error => {
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
    .add-item{
        display: flex;
        justify-content: center;
        align-items: center;
    }
    input{
        background: #f7f7f7;
        border: none;
        padding: 5px;
        margin-right: 10px;
        outline: none;
    }
    button{
        outline: none;
        border-radius: 8px;
        padding: 5px;
        border: unset;
    }
    .active{
        background: #00ce25;
        color: #ffff;
    }
    .inactive{
        color: #9999;
    }
</style>