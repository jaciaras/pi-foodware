<template>
    <div class="items-list">
        <Loading v-if="isLoading" />
        <Item v-for="item in itemsList" :key="item.id" :item="item" />
    </div>
</template>

<script>
import axios from 'axios';
import Item from './Item';
import Loading from './Loading';
export default {
    name: 'ItemsList',
    components: {
        Item,
        Loading  
    },
    data() {
        return {
            itemsList: [],
            isLoading: false
        }
    },
    created() {},
    computed: {
        selectedCategory: {
            get() {
                return this.$store.state.selectedCategory;
            }
        }
    },
    methods: {
        getItemsList() {
            this.isLoading = true;
            this.itemsList = [];
            setTimeout( () => {
                axios.get(`http://localhost:3000/${this.selectedCategory}`).then((response) => {
                    this.itemsList = response.data;
                    this.isLoading = false;
                });
            }, 300);
        }
    },
    watch: {
        selectedCategory() {
            this.getItemsList();
        }
}};
</script>

<style style="less" scoped>
    .items-list {
        width: 100%;
        margin: 50px;
        display: flex;
        flex-wrap: wrap;
        align-content: flex-start;

        @media @tablets {
        flex-wrap: wrap;
        margin: 20px;
        margin: 0px;
        padding: 20px;
    }
    }
</style>