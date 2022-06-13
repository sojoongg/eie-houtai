<template>
  <el-form :model="formData" label-width="120px">
    <el-form-item label="运单号">
      <el-input v-model="formData.DOrder" />
    </el-form-item>

    <el-form-item label="客户 ID">
      <el-input v-model="formData.customerID" />
    </el-form-item>

    <el-form-item>
      <el-button type="primary" @click.prevent="onSubmit">确认到库</el-button>
      <el-button @click="onCancel">Cancel</el-button>
    </el-form-item>
  </el-form>

  <!-- <el-table :data="tableData" style="width: 100%">
    <el-table-column fixed prop="date" label="Date" width="150" />
    <el-table-column prop="address" label="运单号" width="600" />
    <el-table-column prop="name" label="运输公司" width="120" />
    <el-table-column prop="state" label="客户ID" width="120" />
    <el-table-column prop="city" label="订单类型" width="120" />

    <el-table-column fixed="right" label="操作" width="120">
      <template #default>
        <el-button link type="primary" size="small" @click="handleClick"
          >Detail</el-button
        >
        <el-button link type="primary" size="small">Edit</el-button>
      </template>
    </el-table-column>
  </el-table> -->
</template>

<script >
// import { reactive } from "vue";

export default {
  props: ["DOrder", "customerID"],

  data() {
    return {
      formData: {
        DOrder: "",
        customerID: "",
      },
      // tableData: [
      //   {
      //     date: "2016-05-03",
      //     name: "Tom",
      //     state: "California",
      //     city: "Los Angeles",
      //     address: "No. 189, Grove St, Los Angeles",
      //     zip: "CA 90036",
      //     tag: "Home",
      //   },
      // ],
    };
  },

  methods: {
    onSubmit() {
      console.log(this.formData);
    },
    onCancel() {
      console.log("reset form item");
      this.formData = "";
    },
  },
  // do not use same name with ref
  // var formData = reactive({
  //   name: "",
  //   customerID: "",
  // }),

  // const onSubmit = () => {
  //   console.log("submit!");
  // };
};
</script>

<style scoped>
</style>