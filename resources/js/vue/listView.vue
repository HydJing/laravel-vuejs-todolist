<template>
    <div>
        <div v-for="(item, index) in items" :key="index">
            <list-item 
                :item="item"
                 class="item" 
                 v-on:itemchanged="$emit('reloadelist')"
            />
        </div>
    </div>
</template>

<script>
import listItem from "./listItem";
import ListItem from "./listItem.vue";

export default {
    props: ['items'],
    components: {
        listItem
    },
    data: function() {
        return {
            items: []
        }
    },
    methods: {
        getList() {
            axios.get('api/items')
            .then(response => {
                this.items = response.data
            })
            .catch(error => {
                console.log(error)
            })
        }
    },
    created() {

    }
}
</script>

<style scoped>
.item {
    background: #e6e6e6;
    padding: 5px;
    margin-top: 1px;
}
</style>