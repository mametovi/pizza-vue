<template>
  <div>
    <div class="block">
      <div class="container">
        <div class="fix">
      <div class="block-wrap"
        v-for="(item, key) in todos"
        :key="key"
        
        :class="{ active: item.completed, temp: item.temp, sub: item.sub }"
      >
      
      <div class="block-img__wrap d-flex align-items-center justify-content-center">
        
        <div class="block-img" :class="['size-'+pizzaSize, ingrClass]">
          <img src="../assets/pizza-3.png" alt="" class="pizza">
          
          <div class="ingridient-img">

            <div v-for="(ingr, key) in ingridietns" :key="key" :class="['ingridient-item',  `ingridient-item-${ingr.name}`]">            
              <img v-for="(img, key) in ingr.parts" :key="key" :src=" getImgUrl(ingr.name+'-'+img)" alt="" :class="['ingridient-part', `ingridient-part-${key+1}`]">              
            </div>

          </div>
        </div>
      </div>

      <div class="text-center d-flex justify-content-center align-items-center">
          <div class="bsk">$</div>          
          {{ getTotalSum }}        
      </div>

      <div class="block-link d-flex justify-content-center">
        <div v-for="(item, key) in sizes" :key="key">         
          <button class="btn" @click="getSelect(item)" :class="{'btn-primary': item.isActive}">{{ item.title }}</button>
        </div>
      </div>

      <div class="block-icon"> 
        <div class="block-icon__item d-flex justify-content-center">
          <div class="block-item" v-for="(item, key) in ingridietns " :key="key" 
            @click="getSelectIngridient(item)" 
            :class="{'actived': getActiveClass(item, selectedIngrs)}">
            <img :src="item.img">
          </div>
        </div>

      <div class="ps-basket">
        <img src="../assets/img/icons/icon-bs.svg" alt="">
      </div>

      </div>
                  
      </div>
    </div>
    </div>
    </div>
  </div>
</template>


<script>

export default {
  name: "Home",
  
  data() {
    return {
      newTodoText: "",
      pizzaSize: 'm',
      sum: 10,
      ingridietn: '',
      tweenedNumber: 0,
      todos: [
        {
          id: 1,
          completed: false,
          temp: false,
          sub: false
        },
      ],

      sizes: [{
        title: 's',        
        isActive: false,
        sum: 6,
      }, {
        title: 'm',        
        isActive: true,
        sum: 10
      }, {
        title: 'l',
        isActive: false,
        sum: 15
      }],

      ingridietns: [{
        title: 1,
        img: require("../assets/img/icons/icon-gr.svg"),
        actived: false,
        sum: 1,
        name: 'moshrous',
        parts: 4
      }, {
        title: 2,
        img: require("../assets/img/icons/icon-cream.svg"),
        actived: false,
        sum: 1,
        name: 'olivki',
        parts: 3
      }, {
        title: 3,
        img: require("../assets/img/icons/icon-bow.svg"),
        actived: false,
        sum: 1,
        name: 'pi',
        parts: 4
      }, {
        title: 4,
        img: require("../assets/img/icons/icon-cucumbers.svg"),
        actived: false,
        sum: 1,
        name: 'og',
        parts: 4
      }, {
        title: 5,
        img: require("../assets/img/icons/icon-peas.svg"),
        actived: false,
        sum: 1,
        name: 'gor',
        parts: 3
      }, {
        title: 6,
        img: require("../assets/img/icons/icon-potatoes.svg"),
        actived: false,
        sum: 1,
        name: 'car',
        parts: 4
      }, {
        title: 7,
        img: require("../assets/img/icons/icon.peper.svg"),
        actived: false,
        sum: 1,
        name: 'peper',
        parts: 4
      }],
      
      selectedIngrs: [],
      ingrClass: []
      
    };
  },

  computed: {
    getTotalSum() {
      let total = this.sum
      
      const size = this.sizes.find((el) => {
        return el.isActive;
      })

      total += size.sum

      const ingrs = this.ingridietns.filter((rel) => {
        return rel.actived;
      })
       

      if(ingrs.length) { 
        for(let i in ingrs) {
          total += ingrs[i].sum
        }
      }

      return total
    }
  },

  methods: {
    getImgUrl(pet) {
      var images = require.context('../assets/images/', false, /\.png$/)
      return images('./' + pet + ".png")
    },

     addNewTodo: function () {
      
      if (this.newTodoText) {
        this.todos.push({
          completed: false,
          temp: false,
          sub: false
        });
      }


      if(this.newTodoText =  this.item.completed) {
        this.todos.push({
          completed: false,
        })
      }

    },



    getSelect(item) {
      const index = this.sizes.indexOf(item)

      for(let i in this.sizes) {
        if(this.sizes[i].isActive === true) {
          this.sizes[i].isActive = false
        }
      }

      this.sizes[index].isActive = true
      this.pizzaSize = this.sizes[index].title

      // this.totalSum = this.sizes[index].sum + this.sum
    },

    getSeconTos(item) {
      const index = this.sizes.indexOf(item)
      
      this.totalSum = this.sizes[index].sum + this.sum

      this.totalSum = this.sizes[index]
    },


    getSelectIngridient(item) {
      
      if(this.selectedIngrs.indexOf(item) < 0){
        this.selectedIngrs.push(item)
        this.ingrClass.push(item.name)
      } else{
        const index = this.selectedIngrs.indexOf(item)
        this.selectedIngrs.splice(index, 1)

        const nameIndex = this.ingrClass.indexOf(item.name)
        this.ingrClass.splice(nameIndex, 1)
      } 
    },

    getActiveClass(item, array) {
      return array.indexOf(item) < 0 ? false : true 
    }

  },

};
</script>
