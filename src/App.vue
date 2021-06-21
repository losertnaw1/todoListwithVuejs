<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- <div id="main"> -->
    <b-card class="main">
      <h1>Todo App</h1>
      <b-list-group>
        <div class="input">
          <b-input-group class="mt-3">
            <b-form-input
              v-model="newTask"
              placeholder="Add your name todo"
            ></b-form-input>
            <b-input-group-append>
              <b-button class="add" @click="add()">+</b-button>
            </b-input-group-append>
          </b-input-group>
        </div>
        <b-list-group-item
          style="border-radius:5px;"
          v-bind:class="[item.completed == true ? 'completed' : 'uncompleted']"
          @click="completed(item)"
          class="item"
          v-for="(item, index) in tasks"
          :key="index"
        >
          <demo1 
          :item="item"
          @del="del(item)"
          />
        </b-list-group-item>
        <div class="footer">
          <p id="all-task">You have {{ count }} pending tasks</p>
          <b-button @click="clearAll()" class="clear-all">Clear all</b-button>
        </div>
      </b-list-group>
    </b-card>
  </div>
</template>

<script>
/* import HelloWorld from './components/HelloWorld.vue' */
import demo1 from "./components/demo1.vue";

export default {
  name: "App",
  components: {
    demo1
  },
  data() {
    return {
      count: 1,
      tasks: [{ id: 1, completed: false, title: "Làm Todo List" }],
      newTask: ""
    };
  },
  methods: {
    clearAll() {
      this.tasks.splice(0, this.count);
      this.tasks =[];
      this.count = 0;
    },
    add() {
      if (this.newTask != "") {
        this.tasks.push({
          title: this.newTask,
          id: (this.count += 1),
          completed: false
        });
      }
      this.newTask = "";
    },
    completed(item) {
      if (item.completed == false) {
        item.completed = true;
        if (this.count >= 1) {
          this.count -= 1;
        }
      } else {
        item.completed = false;
        this.count += 1;
      }
    },
    del(item) {
      // console.log(this.tasks);
      // console.log(e);
      // e.splice(e.id,1)
      const ID = item.id;
      const index = this.tasks.findIndex(i => i.id === ID);
      if (index > -1) {
        if (this.completed == true) {
          this.tasks.splice(index,1)
        } else {
          this.tasks.splice(index,1)
          if (item.id >= 1) {
            this.count -= 1;
          }
        }
      }
    },
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

.main {
  background-color: white;
  max-width: 500px;
  margin: auto;
  border-radius: 6px;
  padding: 10px 0;
}

.input {
  border-radius: 6px;
  padding: 10px 0;
}

.list-group-item {
  background-color: rgb(150, 150, 150);
  margin-bottom: 10px;
}

button.add {
  width: 50px;
  font-size: 25px;
  background-color: rgb(163, 20, 220);
}

.btn-delete {
  position: absolute;
  top: 0;
  right: 0;
  display: none;
}

p#all-task {
  text-align: left;
  /* margin: auto; */
  padding-top: 5px;
  padding-bottom: 5px;
  margin-top: 5px;
  margin-bottom: 5px;
  margin-right: 261.806px;
  margin-left: 0px;
}

body {
  width: 100vw;
  height: 100vh;
  background-image: linear-gradient(#1dc4ca, #036ffc);
}

div.completed {
  text-decoration-line: line-through;
}

.item:hover .btn-delete {
  display: block;
}

.item:hover {
  text-decoration-line: line-through;
}

.footer {
  display: inline-flex;
  border-radius: 10px;
}

button.clear-all {
  position: absolute;
  right: 16px;
  font-size: 20px;
  background-color: rgb(163, 20, 220);
  color: white;
  border-radius: 5px;
}
</style>
