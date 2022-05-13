<template>
  <div>
    <input v-model="inputValue" type="text" />

    <h2>Counter = {{ counter }}</h2>
    <button @click="counter++">Increment counter</button>

    <h2>Count el in massiv = {{ list.length }}</h2>
    <!-- <h2>Double el in massiv = {{doubleLength()}}</h2> -->
    <h2>Double computed el in massiv = {{ doubleLengthCom }}</h2>
    <button @click="list.push(list.length + 1)">Add to massiv</button>

    <div :key="item" v-for="item in list">{{ item }}</div>

    <input v-model="user.address.street" type="text" />

    <div v-if="counter < 3">Block 1</div>
    <div v-else>Block 2</div>

    <div v-show="counter < 3">Block 3</div>
    <div v-show="counter > 3">Block 4</div>

    <!-- <h2>Counter with mixin = {{ counter }}</h2>
    <button @click="increment">Increment counter</button> -->

    <input v-model.number="inputValue2" type="text" />
    <input v-model.trim="inputValue3" type="text" />

    <button @click="list2.push(list2.length + 1)" class="btn">Add item</button>
    <transition-group name="list" tag="div">
      <div v-for="item in list2" :key="item" class="item">{{ item }}</div>
    </transition-group>

    <child style="border: 1px solid green; margin-top: 10px; padding: 5px" />

    <div :class="{ green: toggle }" class="height100">
      <button @click="toggle = !toggle">Toggle</button>
    </div>

    <div :style="{ backgroundColor: color }" class="height100">
      <button @click="toggle2">Toggle 2</button>
    </div>

    <div style="border: 1px solid green; margin-top: 10px">
      <card>
        <template v-slot:header>Title card</template>
        <template v-slot:body>Body card</template>
        <template v-slot:actions>
          <button>Ok</button>
          <button>Cancel</button>
        </template>
      </card>
    </div>

    <div style="margin-top: 10px">
      <input ref="inputref" type="text">
      <button @click="getRef">Get element</button>
    </div>

    <div style="margin-top: 10px; border: 1px solid blue;">
      <button @click="currentComponent = 'FirstComponent'">First</button>
      <button @click="currentComponent = 'SecondComponent'">Second</button>
      <keep-alive>
        <component :is="currentComponent"></component>
      </keep-alive>      
    </div>
    <div style="margin-top: 10px; border: 1px solid gray;">
      <button @click="filter">Filter</button>
      <div v-for="elem in list3" :key="elem">{{elem}}</div>
    </div>

    <div style="margin-top: 10px; border: 1px solid gray;">
      <h2>{{Math.random()}}</h2>
      <button @click="update" >Update</button>
    </div>

  </div>
</template>

<script>
// import CountMixin from "@/CountMixin";
// export default {
// mixins: [CountMixin]
// }
import Child from "@/Child.vue";
import Card from "@/Card.vue";
import FirstComponent from "@/FirstComponent.vue";
import SecondComponent from "@/SecondComponent.vue";
import mixin1 from "@/mixin1";
import mixin2 from "@/mixin2";

export default {
  mixins: [mixin1, mixin2],
  components: { Child, Card, FirstComponent, SecondComponent },
  data() {
    return {
      inputValue: "",
      counter: 0,
      list: [1, 2],
      user: {
        name: "alex",
        address: {
          street: "",
        },
      },
      inputValue2: "",
      inputValue3: "",
      list2: [1, 2, 3, 4],
      toggle: false,
      color: "red",
      currentComponent: 'FirstComponent',
      list3: [1, 2, 3, 4, 5, 6, 7, 8],
    };
  },
  provide() {
    return {
      user: this.user,
    };
  },
  methods: {
    doubleLength() {
      console.log("vizov");
      return this.list.length * 2;
    },
    toggle2() {
      this.color = this.color === "red" ? "green" : "red";
    },
    getRef() {
      this.$refs.inputref.focus()
      console.log(this.$refs.inputref)
    },
    filter() {
     this.list3 = this.list3.filter(elem => elem & 2 !== 0)
    },
    update() {
      this.$forceUpdate() //принудительное обновление компонента
    }
  },
  computed: {
    doubleLengthCom() {
      console.log("vizov");
      return this.list.length * 2;
    },
  },
  watch: {
    counter(newValue) {
      console.log(`change counter ` + newValue);
    },
    inputValue(newValue) {
      console.log(`change input ` + newValue);
    },
    "user.address.street"(newValue) {
      console.log(newValue);
    },
  },
  mounted() {
    console.log('COMPONENT MOUNTED')
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.btn {
  display: flex;
}

.item {
  padding: 20px;
  border: 1px solid orange;
}

.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(400px);
}

.height100 {
  height: 20px;
  margin-top: 10px;
}
.green {
  background-color: green;
}
</style>
