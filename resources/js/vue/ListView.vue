<template>
    <div>
        <div v-for="(item ,index) in items" :key="index">
            <list-item :item="item" :class="item" v-on:itemchanged="$emit('reloadlist')" />
        </div>
    </div>
</template>


<script>
import listItem from './ListItem'
import ListItem from './ListItem.vue'
export default {
    props:['items'],
    components: { ListItem },
    
}
</script>