<template>
  <div id="app">
    <table>
      <thead>
        <tr>
          <th>序号</th>
          <th>名称</th>
          <th>年龄</th>
          <th>手机号</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="v in tableData" :key="v.id" @contextmenu.prevent="openMenu($event, v)">
          <td>{{ v.id }}</td>
          <td>{{ v.name }}</td>
          <td>{{ v.age }}</td>
          <td>{{ v.phone }}</td>
        </tr>
      </tbody>
    </table>
    <context-menu class="right-menu"
      :offset="menuOffset">
      <template v-slot:menuItem>
        <li>{{currentData.id}}</li>
        <li>{{currentData.name}}</li>
        <li>{{currentData.age}}</li>
        <li>{{currentData.phone}}</li>
      </template>
    </context-menu>
  </div>
</template>

<script>
import ContextMenu from '@/component/ContextMenu.vue'
export default {
  name: 'app',
  components: {
    ContextMenu
  },
  data () {
    return {
      menuOffset: {
        offsetLeft: 0,
        offsetWidth: 0,
        clientX: 0,
        clientY: 0
      },
      currentData: {},
      tableData: [{
        id: 1,
        name: 'test1',
        age: 11,
        phone: 14141411111
      }, {
        id: 2,
        name: 'test2',
        age: 22,
        phone: 14141411111
      }, {
        id: 3,
        name: 'test3',
        age: 33,
        phone: 14141411111
      }, {
        id: 4,
        name: 'test4',
        age: 44,
        phone: 14141411111
      }]
    }
  },
  methods: {
    openMenu (e, data) {
      console.log(data)
      this.menuOffset.offsetLeft = this.$el.getBoundingClientRect().left // container margin left
      this.menuOffset.offsetWidth = this.$el.offsetWidth // container width
      this.menuOffset.clientX = e.clientX
      this.menuOffset.clientY = e.clientY
      this.currentData = data
    }
  }
}
</script>

<style scoped>
table {
  width: 100%;
  text-align: center;
}
table td,
table th {
  padding: 20px;
  border: 1px solid #dfdfdf;
}
</style>
