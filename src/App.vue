<template>
  <div id="app" class="container">
    <h1 class="header">Vue Todos</h1>
    <table>
      <thead class="head">
        <tr>
          <th>
            <input
              type="checkbox"
              id="checkbox"
              @input="toggleAll"
              :checked="doneAll"
              :indeterminate.prop="!doneAll && !notDoneAll"
            />
          </th>
          <th>タスク名</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in items" :key="item.id">
          <td>
            <input type="checkbox" v-model="item.selected" />
          </td>
          <td>{{ item.name }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { id: 1, name: "タスク1", selected: false },
        { id: 2, name: "タスク2", selected: false },
        { id: 3, name: "タスク3", selected: false }
      ]
    };
  },
  computed: {
    doneAll() {
      if (
        this.items.every(item => {
          return item.selected;
        })
      ) {
        return true;
      }

      return false;
    },
    notDoneAll() {
      if (
        this.items.every(item => {
          return !item.selected;
        })
      ) {
        return true;
      }

      return false;
    }
  },
  methods: {
    toggleAll() {
      if (this.doneAll) {
        this.items.forEach(item => {
          item.selected = false;
        });
      } else {
        this.items.forEach(item => {
          item.selected = true;
        });
      }
    }
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

.container {
  display: flex;
  flex-direction: column;
  width: 100%;
  justify-content: center;
  align-items: center;
}

.header {
  display: inline;
}

table {
  border-collapse: collapse;
}

th {
  border-bottom: solid 3px rgba(63, 58, 58, 0.15);
}

tr + tr {
  border-top: solid 1px rgba(63, 58, 58, 0.15);
}
</style>
