<template>
    <div class="single-item">
        <input type="checkbox" @click="updateCheck()" v-model="item.completed">
        <span :class="[item.completed ? 'completed' : '', 'item-text']">{{ item.name }}</span>
        <button @click="removeItem()">Remove</button>
    </div>
</template>


<script>
export default {
    props: ['item'],
    methods:{
        updateCheck(){
            console.log(this.item.completed);
            axios.put('api/item/'+ this.item.id,{
                item: this.item
            })
            .then(Response => {
                if(Response == 200){
                    this.$emit('itemchanged');
                }
            })
            .catch(error =>{
                cosnole.log(error);
            })
        },
        removeItem(){
            axios.delete('api/item/'+ this.item.id,{
                item: this.item
            })
            .then(Response => {
                if(Response == 200){
                    this.$emit('itemchanged');
                }
            })
            .catch(error =>{
                cosnole.log(error);
            })
        }
    }
}
</script>

<style scoped>
button{
    border: none;
    color: #ffffff;
    background: orangered;
    float: right;
}
.completed{
    text-decoration: line-through;
    color: green;
}
</style>