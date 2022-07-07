<template>
  <div>
    <MyTable :arr="list">
      <template #header>
        <th>#</th>
        <th>商品名称</th>
        <th>价格</th>
        <th>标签</th>
        <th>操作</th>
      </template>
      <template #tbody="scope">
        <td>{{ scope.obj.id }}</td>
        <td>{{ scope.obj.goods_name }}</td>
        <td>{{ scope.obj.goods_price }}</td>
        <td>
          <input
            class="tag-input form-control"
            style="width: 100px"
            type="text"
            v-gfocus
            v-model="scope.obj.inputValue"
            @keydown.esc="scope.obj.inputValue = ''"
            @blur="scope.obj.inputVisible = false"
            @keydown.enter="enterFn(scope.obj)"
            v-if="scope.obj.inputVisible"
          />
          <button
            v-else
            style="display: block"
            class="btn btn-primary btn-sm add-tag"
            @click="scope.obj.inputVisible = true"
          >
            +Tag
          </button>
          <span
            style="margin-right: 8px"
            class="badge badge-warning"
            v-for="(item, index) in scope.obj.tags"
            :key="index"
            >{{ item }}</span
          >
        </td>
        <td>
          <button class="btn btn-danger btn-sm" @click="del(scope.obj.id)">
            删除
          </button>
        </td>
      </template>
    </MyTable>
  </div>
</template>

<script>
import MyTable from '../components/MyTable.vue';
export default {
  name: 'New7MyGoodsList',
  created() {
    this.$axios({
      url: '/api/goods',
    }).then((res) => {
      console.log(res);
      this.list = res.data.data;
    });
  },
  data() {
    return {
      list: [],
    };
  },

  mounted() {},
  components: {
    MyTable,
  },
  methods: {
    del(id) {
      let index = this.list.findIndex((item) => item.id == id);
      this.list.splice(index, 1);
    },
    enterFn(obj) {
      // 回车
      console.log(obj.inputValue);
      if (obj.inputValue.trim().length === 0) {
        alert('请输入数据');
        return;
      }

      obj.tags.push(obj.inputValue); // 表单里的字符串状态tags数组
      obj.inputValue = '';
    },
  },
};
</script>

<style lang="scss" scoped></style>
