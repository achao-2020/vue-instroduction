<template>
  <h2>表单组件练习</h2>
  <el-row>
    <el-col :span="8">
      <el-input v-model="queryName" placeholder="请输入搜索内容"> </el-input>
    </el-col>
    <el-col :span="2">
      <el-button type="primary" @click="search">搜索</el-button>
      <!-- 添加按钮 -->
      <el-button type="primary" @click="addVisiable = true">添加</el-button>
    </el-col>
    <!-- 添加弹出对话框 -->
    <el-dialog v-model="addVisiable" append-to-body>
      <el-form
        :model="addData"
        label-width="120px"
        :tableForm="tableForm"
        v-if="addVisiable"
      >
        <el-form-item label="名称">
          <el-input v-model="addData.name" />
        </el-form-item>
        <el-form-item label="金额">
          <el-input v-model="addData.money" />
        </el-form-item>
        <el-form-item label="类型">
          <el-input v-model="addData.type" />
        </el-form-item>
        <span>
          <el-button type="primary" plain @click="addVisiable = false">
            取消
          </el-button>
          <el-button type="primary" @click="addTableData"> 确认 </el-button>
        </span>
      </el-form>
    </el-dialog>
  </el-row>
  <!-- 更新弹出对话框 -->
  <el-dialog v-model="updateVisiable" append-to-body>
    <el-form
      :model="addData"
      label-width="120px"
      :tableForm="tableForm"
      v-if="updateVisiable"
    >
      <el-form-item label="名称">
        <el-input v-model="addData.name" />
      </el-form-item>
      <el-form-item label="金额">
        <el-input v-model="addData.money" />
      </el-form-item>
      <el-form-item label="类型">
        <el-input v-model="addData.type" />
      </el-form-item>
      <span>
        <el-button type="primary" plain @click="updateVisiable = false">
          取消
        </el-button>
        <el-button type="primary" @click="updateTableData"> 确认 </el-button>
      </span>
    </el-form>
  </el-dialog>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column prop="name" label="名称" />
    <el-table-column prop="money" label="金额" />
    <el-table-column prop="type" label="类型" />
    <el-table-column label="操作">
      <!-- 汽包确认框 -->
      <template v-slot="scop">
        <el-button type="primary" @click="activeUpdate(scop.$index)"
          >更改</el-button
        >
        <el-popconfirm title="确认删除?" @confirm="delTableData(scop.$index)">
          <template #reference>
            <el-button type="danger">删除</el-button>
          </template>
        </el-popconfirm>
      </template>
    </el-table-column>
  </el-table>
</template>
  
  <script>
export default {
  data() {
    return {
      // eg:
      // name: '红玫王',
      // money: '14',
      // type: '烟酒',
      tableData: [{ name: "红玫王", money: 14, type: "烟酒" }],
      addData: [],
      addVisiable: false,
      updateVisiable: false,
      updateIndex: 0,
      delConfirm: false,
      queryName: "",
    };
  },

  methods: {
    addTableData() {
      this.addVisiable = false;
      var len = this.tableData.length;
      this.tableData.push({
        name: this.addData.name,
        money: this.addData.money,
        type: this.addData.type,
      });
    },

    delTableData(index) {
      console.log(index);
      this.tableData.splice(index, 1);
    },

    activeUpdate(index) {
      this.updateVisiable = true;
      this.updateIndex = index;
      this.addData = this.tableData[index];
    },

    updateTableData(data) {
      this.tableData[this.updateIndex].name = this.addData.name;
      this.tableData[this.updateIndex].money = this.addData.money;
      this.tableData[this.updateIndex].type = this.addData.type;
      this.updateVisiable = false;
    },

    search() {
      this.tableData = this.tableData.filter((data) => {
        if (data.name == this.queryName) {
          return data;
        }
      });
    },
  },
};
</script>
  