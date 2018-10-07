<template>
  <div id="app">
    <div class="container">
      <input type="text" v-model="newTaskName" />
      <select v-model="newTaskAssignee">
        <option value="🐱">🐱</option>
        <option value="🐶">🐶</option>
        <option value="🐹">🐹</option>
      </select>
      <input type="number" v-model="newTaskMandays">
      <button @click="addTask">追加</button>
      <hr>
      <div class="columns">
        <div class="column status-1">
          <div class="tags has-addons">
            <span class="tag">未対応</span>
            <span class="tag is-dark">{{ tasksOpen.length }}</span>
          </div>
          <transition-group name="fade">
          <div class="card" v-for="task in tasksOpen" v-bind:key="task.name">
            <div class="card-content">{{ task.name }}</div>
            <div class="card-footer">
              <div class="card-footer-item">{{ task.assignee }}</div>
              <div class="card-footer-item">{{ task.mandays }} 人日</div>
            </div>
            <div class="card-footer">
              <a class="card-footer-item" v-on:click="decrementStatus(task)">◀︎</a>
              <a class="card-footer-item" v-on:click="incrementStatus(task)">▶︎</a>
            </div>
          </div>
          </transition-group>
        </div>
        <div class="column status-2">
          <div class="tags has-addons">
            <span class="tag">処理中</span>
            <span class="tag is-dark">{{ tasksDoing.length }}</span>
          </div>
          <transition-group name="fade">
          <div class="card" v-for="task in tasksDoing" v-bind:key="task.name">
            <div class="card-content">{{ task.name }}</div>
            <div class="card-footer">
              <div class="card-footer-item">{{ task.assignee }}</div>
              <div class="card-footer-item">{{ task.mandays }} 人日</div>
            </div>
            <div class="card-footer">
              <a class="card-footer-item" v-on:click="decrementStatus(task)">◀︎</a>
              <a class="card-footer-item" v-on:click="incrementStatus(task)">▶︎</a>
            </div>
          </div>
        </transition-group>
        </div>
        <div class="column status-3">
          <div class="tags has-addons">
            <span class="tag">完了</span>
            <span class="tag is-dark">{{ tasksClosed.length }}</span>
          </div>
          <transition-group name="fade">
          <div class="card" v-for="task in tasksClosed" v-bind:key="task.name">
            <div class="card-content">{{ task.name }}</div>
            <div class="card-footer">
              <div class="card-footer-item">{{ task.assignee }}</div>
              <div class="card-footer-item">{{ task.mandays }} 人日</div>
            </div>
            <div class="card-footer">
              <a class="card-footer-item" v-on:click="decrementStatus(task)">◀︎</a>
              <a class="card-footer-item" v-on:click="incrementStatus(task)">▶︎</a>
            </div>
          </div>
        </transition-group>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
var filters = {
	open: function (tasks) {
  	return tasks.filter(function (task) {
    	return task.status === 1
    })
  },
	doing: function (tasks) {
  	return tasks.filter(function (task) {
    	return task.status === 2
    })
  },
  closed: function (tasks) {
  	return tasks.filter(function (task) {
    	return task.status === 3
    })
  }
}
export default {
  data: function () {
    return {
        tasks: [
          {name: "task1", status: 1, assignee: "🐱", mandays: "4"},
          {name: "task2", status: 1, assignee: "🐱", mandays: "4"},
          {name: "task3", status: 2, assignee: "🐱", mandays: "4"},
          {name: "task4", status: 3, assignee: "🐱", mandays: "5"},
        ],
        newTaskName: '',
        newTaskAssignee: null,
        newTaskMandays: 0
    }
  },
  methods: {
    incrementStatus: function (task) {
      if(1 <= task.status && task.status <= 2) {
        task.status++
      }
    },
    decrementStatus: function (task) {
      if(2 <= task.status && task.status <= 3) {
        task.status--
      }
    },
    addTask(){
      this.tasks.push({ name: this.newTaskName, status: 1, assignee: this.newTaskAssignee, mandays: this.newTaskMandays })
    }
  },
  computed: {
    tasksOpen: function () {

      return this.tasks.filter(function (task) {
      	return task.status === 1;
      });

      //return filters.open(this.tasks)
    },
    tasksDoing: function () {
      return this.tasks.filter(function (task) {
      	return task.status === 2
      });
      //return filters.doing(this.tasks)
    },
    tasksClosed: function () {
      return this.tasks.filter(function (task) {
      	return task.status === 3
      });
      //return filters.closed(this.tasks)
    }
  }
}
</script>

<style>
.status-1 {
  background-color: #ed8077;
}
.status-2 {
  background-color: #4488c5;
}
.status-3 {
  background-color: #5eb5a6;
}
.card {
  margin-bottom: 5px;
}
.card-footer-item {
  padding-top: 0px;
  padding-bottom: 0px;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.7s
}
.fade-enter, .fade-leave-to {
  opacity: 0
}
</style>
