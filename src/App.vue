<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>
  <!--  -->
  <div class="row justify-content-center">
    <form class="col-6 col-md-4" action="" id="formApp">
      <div>
        <h2>{{formHeader}}</h2>
      </div>
      <div class="formContainer">
<!--        <form-item-->
<!--            v-for="item in formItems"-->
<!--            v-bind:item="item"-->
<!--            v-bind:key="item.id"-->

<!--            v-on:move-left="moveLeft"-->
<!--            v-on:move-right="moveRight"-->
<!--        >-->
        <form-item
            v-for="item in test"
            v-bind:item="item"
            v-bind:key="item.id"

            v-on:move-left="moveLeft"
            v-on:move-right="moveRight"
        >
          <!-- сюда поля -->
          <form-input
              v-for="input in item.inputs"
              :input="input"
          >

          </form-input>
          <!-- сюда поля -->
        </form-item>
      </div>
    </form>
  </div>
  <!--  -->
</template>

<script>
import FormItem from "@/components/FormItem";
// import FormInput from "@/components/UI/FormInput";
export default {
  mounted() {
    this.appendInputs;
  },
  components: {
    FormItem,
    // FormInput,
  },
  data() {
    return {
      formHeader: "Конструктор заказа",
      inputsPerPage: 2,
      test: [],
      formInputs: [
        { id:0, type:'text',  },//
        { id:1, type:'text',  },//
        { id:2, type:'number',  },//
      ],
      formItems: [
        {
          id: 0,
          title:'Title 1',
          visible: true,
          position: {top:0,left:0  },
          order:{
            first:true,
            last:false,
            current:true
          },
        },
        {
          id: 1,
          title:'Title 2',
          visible: false,
          position: {top:0,left:301},
          order:{
            first:false,
            last:false,
            current:false
          },
        },
        {
          id: 2,
          title:'Title 3',
          visible: false,
          position: {top:0,left:301},
          order:{
            first:false,
            last:false,
            current:false
          },
        },
        {
          id: 3,
          title:'Title 4',
          visible: false,
          position: {top:0,left:301},
          order:{
            first:false,
            last:true,
            current:false
          },
        },
      ],
    }
  },
  computed: {
    appendInputs() {
      let inputs = this?.formInputs.slice();
      let inputsPerPage = this?.inputsPerPage;
      let pageCount =  Math.round(inputs?.length/inputsPerPage); // кол-во страниц конструктора
      let result = []; // результат
      let currentId = 0; // текущий id для заполнения атрибута с полями (объекта страницы)
      for (let i = 0; i < pageCount; i++) {
        // result?.push({
        this.test?.push({
          // непосредственно объект одной страницы
          id:         i,
          title:      'Title ' + i,
          visible:    (i === 0),
          position:   (i === 0)? {top:0,left:0}:{top:0,left:301}, // позиция для первого, и для остальных элементов
          order:      {first:(i===0), last:(i===(pageCount-1)), current:(i===0)}, // условия для определения первого и последнего объектов
          inputs:     []
        });
        while (inputs.length !== 0) {
          // заполнение атрибута полями
          if (this.test[i]?.inputs?.length === inputsPerPage) {
            // если длина массива в объекте страницы равна кол-ву полей на странице (inputsPerPage)
            // то цикл переходит к заполнению след. объекта страницы
            break;
          }
          // заполнение объекта (модели приложения) и затем
          // удаления отправленного элемента из локального массива полей
          this.test[i]?.inputs?.push(inputs[0]);
          inputs.shift();
        }
      }
      // return result;
    },
  },
  methods: {
    moveLeft(id) {
      // this.formItems[id].position.left -= 301;
      // this.formItems[id].order.current = false;
      // this.formItems[id].visible = false;
      //
      // this.formItems[id+1].visible = true;
      // this.formItems[id+1].position.left -= 301;
      // this.formItems[id+1].order.current = true;
      this.test[id].position.left -= 301;
      this.test[id].order.current = false;
      this.test[id].visible = false;

      this.test[id+1].visible = true;
      this.test[id+1].position.left -= 301;
      this.test[id+1].order.current = true;
      // console.log(this.formItems[id])
    },
    moveRight(id) {
      // this.formItems[id].visible = false;
      // this.formItems[id-1].visible = true;
      // this.formItems[id].position.left += 301;
      // this.formItems[id-1].position.left += 301;
      this.test[id].visible = false;
      this.test[id-1].visible = true;
      this.test[id].position.left += 301;
      this.test[id-1].position.left += 301;
    },
    // isFirst(id) {
    //     let arr = this.formItems
    //     result = arr.shift()
    //     return result === this.formItems[id] && this.formItems[id].current === true
    // },
    // isLast() {
    //     let arr = this.formItems
    //     result = arr[arr.length-1]
    //     return result === this.formItems[id] && this.formItems[id].current === true
    // },

  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
/**/
.formContainer {
  display: flex;
  overflow: hidden;
}
.formItem {
  position: relative;
  width: 300px !important;
  height: 450px;
}
.none {
  display: none;
}
</style>
