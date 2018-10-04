<template>
  <div id="app">
    <div class="container">
      <div class="columns">
        <div class="column status-1">
          <div class="tags has-addons">
            <span class="tag">未対応</span>
            <span class="tag is-dark">{{ tasks.length }}</span>
          </div>
          <div class="card" v-for="task in tasks" v-bind:key="task.name">
            <div class="card-content">{{ task.name }}</div>
            <div class="card-footer">
              <div class="card-footer-item">{{ task.assignee }}</div>
              <div class="card-footer-item">{{ task.mandays }} 人日</div>
            </div>
            <div class="card-footer">
              <a class="card-footer-item">◀︎</a>
              <a class="card-footer-item">▶︎</a>
            </div>
          </div>
        </div>
        <div class="column status-2">
          <div class="tags has-addons">
            <span class="tag">処理中</span>
            <span class="tag is-dark"></span>
          </div>
        </div>
        <div class="column status-3">
          <div class="tags has-addons">
            <span class="tag">完了</span>
            <span class="tag is-dark"></span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
        tasks: [
          {name: "task2", status: "2", assignee: "🐱", mandays: "4"},
          {name: "task3", status: "3", assignee: "🐱", mandays: "5"},
        ],
    }
  }
}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}
</style>
