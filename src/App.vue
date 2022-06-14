<template>
  <el-form :model="{ formData }" label-width="120px">
    <el-form-item label="运单号">
      <el-input ref="DOrder" v-model="formData.DOrder" />

      <strong v-if="this.errors.length" style="color: red"
        >Please enter the Delivery Order</strong
      >
    </el-form-item>

    <el-form-item label="客户 ID">
      <el-input v-model="formData.customerID" />
      <strong v-if="this.errors.length" style="color: red"
        >Please enter the Customer ID</strong
      >
    </el-form-item>

    <el-form-item>
      <el-button type="primary" @click="checkForm">确认到库</el-button>
      <el-button @click="onCancel">清除</el-button>
    </el-form-item>
  </el-form>

  <div class="container">
    <el-table :data="tableData" style="width: 100%">
      <el-table-column type="index" prop="index" label="序号" width="150" />
      <el-table-column prop="deliveryOrder" label="运单号" width="600" />
      <el-table-column prop="companyName" label="运输公司" width="120" />
      <el-table-column prop="customerID" label="客户ID" width="120" />
      <el-table-column prop="typeOfOrder" label="订单类型" width="120" />

      <el-table-column fixed="right" label="操作" width="120">
        <template #default="scope">
          <el-button link type="primary" size="small">修改信息</el-button>
          <el-button
            link
            type="primary"
            size="small"
            @click="onDel(scope.row, scope.$index)"
          >
            删除
          </el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script >
// import { reactive } from "vue";

export default {
  data() {
    return {
      formData: {
        DOrder: "",
        customerID: "",
      },
      tableData: [],
      errors: [],
    };
  },

  methods: {
    checkForm(e) {
      e.preventDefault();
      this.errors = [];
      // validate if input field is empty or not
      // validate if input field is empty or not
      // validate if input field is empty or not
      if (!this.formData.DOrder) {
        this.errors.push("The Delivery Order is required");
      }
      if (!this.formData.customerID) {
        this.errors.push("The Customer ID is required");
      }
      // if form is not empty, then submit the form
      // if form is not empty, then submit the form
      // if form is not empty, then submit the form
      if (!this.errors.length) {
        this.onSubmit();
      }
    },
    onSubmit() {
      console.log("form is succefully submitted", this.formData);

      this.tableData.push({
        deliveryOrder: this.formData.DOrder,
        customerID: this.formData.customerID,
      });
    },
    onCancel() {
      console.log("reset form item");
      this.formData = {};
    },
    onDel(tableData, index) {
      console.log("delete this row");
      console.log(this.tableData);
      this.tableData.splice(index, 1);
    },
  },
};
</script>


