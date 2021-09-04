!<template>
    <div class="filter">
        <ul>
            <li 
            class="filter-box" 
            v-for="filterOption in filterOptions"
            v-bind:key="filterOption.filterName"
            v-on:click="switchFilter(filterOption)"
            v-bind:class="{ selected: isSelected(filterOption)}">
            {{ filterOption.filterName }}
            </li>
        </ul>
        <div class="added-filters">
            <span 
            class="added-filter" 
            v-for="addedFilter in addedFilters"
            v-bind:key="addedFilter.filterName">
            {{ addedFilter.filterName }}
            </span>
        </div>
    </div>
</template>

<script>
export default {
    name: "productFilter",
    props: ['filterOptions', 'addedFilters'],
    methods: {
        switchFilter: function(filter){
            if(this.isSelected(filter)){
                this.$emit('removeFilter', filter);
            }else{
                this.$emit('addFilter', filter);
            }
        },
        isSelected: function(filter){
            return this.addedFilters.filter(e => e.filterName === filter.filterName).length > 0;
        }
    }

}
</script>

<style scoped>
    .filter ul{
        display: flex;
        flex-direction: row;
    }
    .filter-box{
        padding: 12px 25px;
        border: 2px solid black;
        margin: 2px;
        width: 4rem;
        user-select: none;
    }
    .filter-box:hover{
        cursor: pointer;
    }
    .selected{
        background: #14c833;
    }
    .added-filters{
        display: flex;
        justify-content: flex-start;
    }
    .added-filter{
        color: lightskyblue;
        text-decoration: underline;
        margin: 5px;
    }
</style>