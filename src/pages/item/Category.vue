<template>
  <v-card>
      <v-flex xs12 sm10>
        <v-tree url="/item/category/list"
                :isEdit="isEdit"
                @handleAdd="handleAdd"
                @handleEdit="handleEdit"
                @handleDelete="handleDelete"
                @handleClick="handleClick"
        />
      </v-flex>
  </v-card>
</template>

<script>
  export default {
    name: "category",
    data() {
      return {
        isEdit:true
      }
    },
    methods: {
      handleAdd(node) {
        console.log("add .... ");
        console.log(node);
          this.$http({
              method: 'post',
              url: '/item/category/add',
              data: this.$qs.stringify(node)       // 这样处理后将直接返回4个对象，而不是Json数据
          }).then(() => {
              this.$message.success("新增成功！");
          })
              .catch(() => {
                  this.$message.error("新增失败！");
              });
      },
      handleEdit(id, name) {
        console.log("edit... id: " + id + ", name: " + name)
          let params = new URLSearchParams();
          params.append("id",id);
          params.append("name",name);
          this.$http.post(
              '/item/category/edit',
              params
          ).then(() => {
              this.$message.success("编辑成功！");
          })
              .catch(() => {
                  this.$message.error("编辑失败！");
              });
      },
      handleDelete(id) {
        console.log("delete ... " + id)
          let params = new FormData();
          params.append("id",id);
          this.$http.delete(
              '/item/category/delete',
              {data: params
              }).then(() => {
              this.$message.success("删除成功！");
          })
              .catch(() => {
                  this.$message.error("删除失败！");
              });

      },
      handleClick(node) {
        console.log(node)
      }
    }
  };
</script>

<style scoped>

</style>
