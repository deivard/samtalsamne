<template>
  <div id="categoriesWrapper" ref="categoriesWrapper"
    :style="{gridTemplateColumns: 'repeat(' + this.gridColumns + ', 1fr)' }"
  >
    <template v-for="(category, index) in categories" >
      <button :key="category"
        :class="'category-' + (index+1)+ (index === 0 ? ' active' : '')"
        :style="{ gridRow: 1}"
        class="text-sm text-hairline w-auto"
        @click="setCategory"
        
      >
        {{ category }}
      </button>
    </template>
  </div>
</template>

<script>
export default {
  name: "CategoriesGroup",
  props: ["categories"],
  data() {
    return {

    }
  },
  computed: {
    gridColumns: function() {
      return this.categories.length
    },
    middleColumnIndex: function() {
      return Math.floor((this.gridColumns / 2) + 1)
    }
  },
  methods: {
    setCategory: function (element) {
      var currentActive = document.getElementsByClassName("active")[0]
      var clickedCategoryIndex = this.getCategoryClassFromList(element.target.classList)
      var currentActiveCategoryIndex = this.getCategoryClassFromList(currentActive.classList)
      // Set the active class to the clicked element
      currentActive.classList.remove("active")
      element.target.classList.add("active")
      // Swap their categoryIndex classes
      this.swapCategoryIndexClasses(clickedCategoryIndex, currentActiveCategoryIndex)
      // ... and place them in the correct columns
      currentActive.style.gridColumn = (clickedCategoryIndex.split("-")[1]) + "/" + (parseInt(clickedCategoryIndex.split("-")[1]) + 1)
      element.target.style.gridColumn =  (currentActiveCategoryIndex.split("-")[1]) + "/" + (parseInt(currentActiveCategoryIndex.split("-")[1]) + 1) 
    },

    // Finds the classes with the two category-index and swap their category-index classes
    swapCategoryIndexClasses: function(categoryIndexA, categoryIndexB) {
      var elementA = document.getElementsByClassName(categoryIndexA)[0];
      var elementB = document.getElementsByClassName(categoryIndexB)[0];
      // Swap
      elementA.classList.remove(categoryIndexA)
      elementA.classList.add(categoryIndexB)
      elementB.classList.remove(categoryIndexB)
      elementB.classList.add(categoryIndexA)
    },
    // Helper function that gets the category-index class of the clicked category
    getCategoryClassFromList: function(classList) {
      for(let className of classList) {
        if (className.includes("category-")) {
          return className
        }
      }
    },
    swapColumns: function(elementA, elementB){
      var elementAColumn = this.getCategoryClassFromList(elementA.classList).split("-")[1]
      var elementBColumn = this.getCategoryClassFromList(elementB.classList).split("-")[1]
      elementA.style.gridColumn = elementBColumn + "/" + (parseInt(elementBColumn)+1)
      elementB.style.gridColumn = elementAColumn + "/" + (parseInt(elementAColumn)+1)
    }

  },
  created() {

  },
  mounted() {

    var activeElement = document.getElementsByClassName("active")[0]//.style.gridColumn = this.middleColumnIndex
    var middleElement = document.getElementsByClassName("category-" + this.middleColumnIndex)[0]
    console.log(activeElement.classList)
    console.log(middleElement.classList)
    this.swapColumns(activeElement, middleElement);
    this.swapCategoryIndexClasses(
      this.getCategoryClassFromList(activeElement.classList),
      this.getCategoryClassFromList(middleElement.classList)
    )
    
  }

}
</script>

<style scoped>

.active {
  font-weight: bold;
  font-size: 1.5em;
}

button:focus {
  outline: none;
}

#categoriesWrapper {
  display: grid;
  grid-template-rows: auto;
}

@media only screen and (max-width: 400px) {
  button {
    font-size: 0.7em;
  }
  .active {
    font-size: 1em;
  }
}
  
</style>
