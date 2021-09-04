<template>
  <div class="container">
    <product-filter :filterOptions="filterOptions" :addedFilters="addedFilters" @addFilter="onFilterAdded($event)" @removeFilter="onFilterRemoved($event)"></product-filter>
    <div class="content">
      <product-box
        v-for="product in shownProducts"
        v-bind:key="product.id"
        v-bind:title="product.title" :product="product">
      </product-box>
      <div v-if="shownProducts.length == 0">
        No hay productos para mostrar
      </div>
    </div>
  </div>
</template>

<script>
import ProductBox from './ProductBox.vue'
import ProductFilter from './ProductFilter.vue'

export default {
  components: { ProductBox, ProductFilter },
  name: 'HelloWorld',
  data: function () {
    return {
      products: [
        { id: 1, title: 'Bejeque', image: 'green_skull.jpg', category: 'skull', color: 'green', size: "3", brilli: "y", },
        { id: 2, title: 'Bejeque', image: 'bejeque.jpg', category: 'cat', color: 'purple', size: "3", brilli: "n" },
        { id: 3, title: 'Bejeque', image: 'bejeque.jpg', category: 'dog', color: 'purple', size: "2", brilli: "y" },
        { id: 4, title: 'Bejeque', image: 'bejeque.jpg', category: 'dog', color: 'red', size: "4", brilli: "n" },
        { id: 5, title: 'Bejeque', image: 'bejeque.jpg', category: 'owl', color: 'purple', size: "2", brilli: "y" },
        { id: 6, title: 'Bejeque', image: 'bejeque.jpg', category: 'owl', color: 'purple', size: "1", brilli: "n" },
        { id: 7, title: 'Bejeque', image: 'bejeque.jpg', category: 'dog', color: 'red', size: "1", brilli: "y" }
      ],
      filterOptions: [{filterName: "Category", options: ["owl"]}, {filterName: "Color", options: ["purple"]}, {filterName: "Size", options: ["1","3"]}, {filterName: "Brilli", options: ["y"]}],
      addedFilters: []
    }
  },
  props: {
    msg: String
  },
  methods: {
    onFilterAdded: function(filter){
      this.addedFilters.push(filter);
    },
    onFilterRemoved: function(filter){
      this.addedFilters = this.addedFilters.filter(e => e.filterName !== filter.filterName);
    },
    isFiltered: function(product){
      var isFiltered = true;
      this.addedFilters.forEach(filter => {
          if(product[filter.filterName.toLowerCase()] && filter.options.length > 0 && !filter.options.includes(product[filter.filterName.toLowerCase()])){
            isFiltered = false;
          }
      });

      return isFiltered;
    }
  },
  computed: {
    shownProducts: function(){
      var shownProducts = [];

      this.products.forEach(product => {
        if(this.isFiltered(product)){
          shownProducts.push(product);
        }
      });

      return shownProducts;
    }
  }
}
</script>

<style scoped>
  .container{
    display: flex;
    justify-content: center;
  }

  .content{
    width: 80%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    flex-wrap: wrap;
  }
</style>
