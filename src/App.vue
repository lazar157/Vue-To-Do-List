<template>
  <div class="outline">
    <section>
      <h1>To do List</h1>
      <input type="text" maxlength="50" placeholder="Add task" v-model.trim="newTask" @keyup.enter="addTask" />
      <button @click="addTask">Add</button>
      <ul>
        <li v-for="(task, index) in tasks" :key="tasks">
          {{ task }}
          <button @click="removeTask(index)" class="red">Remove</button>
        </li>
      </ul>
    </section>
  </div>
</template>


<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: []
    }
  },
  created() {
    const key = 'vue-todo'
    this.tasks = JSON.parse(localStorage.getItem(key) || '[]')
  },
  methods: {
    addTask() {
      if (this.newTask !== '') {
        this.tasks.push(this.newTask)
        this.newTask = ''
      }
      const key = 'vue-todo'
      localStorage.setItem(key, JSON.stringify(this.tasks));
    },
    removeTask(index) {
      this.tasks.splice(index, 1)
      const key = 'vue-todo'
      localStorage.setItem(key, JSON.stringify(this.tasks));
    },
  }
}
</script>



<style>
.outline {
  box-shadow: 0px 6px 11px -5px rgba(0, 0, 0, 0.75);
  padding: 20px 50px;
  border-radius: 25px;
  background-color: rgb(228, 187, 198);
}

body {
  height: 100vh;
  font-family: Roboto;
  display: flex;
  justify-content: center;
  align-items: start;
  background-color: rgb(241, 227, 229);
  background: url(photos/women.jpg);
  backdrop-filter: blur(2.3px);
}



h1 {
  font-size: 50px;
  color: rgb(63, 78, 128);
  font-weight: 900;
  text-align: center;
  text-decoration: underline 0.2rem double;
  font-family: "Pacifico", cursive;
  font-weight: 400;
  font-style: normal;
  transition: 0.5s;
  cursor: pointer;
}

h1:hover {
  color: rgb(91, 112, 182);
}


input {
  border: none;
  font-size: 20px;
  padding: 20px 20px 20px 0;
  text-align: center;
  border-radius: 20px;

}

::placeholder {
  font-size: 20px;
}

button {
  border-radius: 20px;
  font-size: 20px;
  padding: 20px;
  border: none;
  margin-left: 20px;
  cursor: pointer;
  color: rgb(46, 57, 92);
  font-weight: bold;
  background-color: rgb(101, 131, 93);
  transition: 0.5s;
}

button:hover {
  background-color: rgb(78, 156, 56);
}

ul {
  margin: 0;
  padding: 0;
}

li {
  margin-top: 20px;
  list-style-type: none;
  margin-bottom: 24px;
  font-size: 1.5rem;
  border-radius: 20px;
  padding: 5px;
  padding-left: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-weight: 700;
  color: rgb(63, 78, 128);
  background-color: rgb(255, 210, 222);
  font-family: cursive;
}

.red {
  background-color: rgb(218, 76, 76);
  color: rgb(46, 57, 92);
  transition: 0.5s;
}

.red:hover {
  background-color: rgb(221, 17, 17);
}
</style>