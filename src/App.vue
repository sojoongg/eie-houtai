<template>
  <div class="container">
    <el-form :model="{ formData }" label-width="120px">
      <el-form-item label="运单号">
        <el-input v-model="formData.DOrder" />

        <strong v-if="this.errors.length" style="color: red"
          >Please enter a valid Delivery Order</strong
        >
      </el-form-item>

      <el-form-item label="客户 ID">
        <el-input v-model.trim="formData.customerID" />
        <strong v-if="this.errors.length" style="color: red"
          >Please enter a valid Customer ID</strong
        >
      </el-form-item>

      <el-form-item>
        <el-button type="primary" @click="checkForm">确认到库</el-button>
        <el-button @click="onCancel">清除</el-button>
      </el-form-item>
    </el-form>
  </div>

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
        DOrder: null,
        customerID: null,
      },
      tableData: [],
      errors: [],
    };
  },

  methods: {
    checkForm(e) {
      e.preventDefault();

      // 运单号校验
      // 运单号校验
      // 运单号校验
      // 客户ID格式 只能5位数eg：80656
      const customerIDIsValid = /^[0-9]{5}$/;

      // // DHL 运单号格式
      const DHLDOIsValid = /JJD0039[0-9]{5}$|0034[0-9]{5}$/;

      // // DPD 运单号格式
      const DPDDOIsvalid = /0150[0-9]{5}$|0944[0-9]{5}$/;

      // // // UPS 运单号格式
      const UPSDOIsValid = /1Z[0-9]{5}$/;

      // // // Hermes 运单号格式
      const HermesDOIsValid = /H10[0-9]{5}$/;

      // // Amazon 运单号格式
      const AmzDOIsValid = /AA[0-9]{5}$|AB[0-9]{5}$/;

      const DOs = this.formData.DOrder;

      var customerIDResult = customerIDIsValid.test(this.formData.customerID);
      var DHLvalid = DHLDOIsValid.test(DOs) && customerIDResult;
      var DHLvalid2 = DHLDOIsValid.test(DOs);
      var DPDvalid = DPDDOIsvalid.test(DOs) && customerIDResult;
      var DPDvalid2 = DPDDOIsvalid.test(DOs);
      var UPSvalid = UPSDOIsValid.test(DOs) && customerIDResult;
      var UPSvalid2 = UPSDOIsValid.test(DOs);
      var Hermesvalid = HermesDOIsValid.test(DOs) && customerIDResult;
      var Hermesvalid2 = HermesDOIsValid.test(DOs);
      var Amzvalid = AmzDOIsValid.test(DOs) && customerIDResult;
      var Amzvalid2 = AmzDOIsValid.test(DOs);

      // validate if input field is empty or not
      this.errors = [];
      if (!DOs) {
        this.errors.push("The Delivery Order is required");
      }

      // 判断运输公司以及订单类型
      if (DHLvalid || DHLvalid2) {
        this.onSubmitToDHL();
      } else if (DPDvalid || DPDvalid2) {
        this.onSubmitToDPD();
      } else if (UPSvalid || UPSvalid2) {
        this.onSubmitToUPS();
      } else if (Hermesvalid || Hermesvalid2) {
        this.onSubmitTohHermes();
      } else if (Amzvalid || Amzvalid2) {
        this.onSubmitToAmz();
      } else {
        console.log("form is invalid");
      }
    },
    onSubmitToDHL() {
      console.log("form is succefully submitted", this.formData);

      if (!this.formData.customerID) {
        this.tableData.push({
          deliveryOrder: this.formData.DOrder,
          customerID: this.formData.customerID,
          typeOfOrder: "无ID订单",
          companyName: "DHL",
        });
        alert("确定无客户ID");
      } else {
        this.tableData.push({
          deliveryOrder: this.formData.DOrder,
          customerID: this.formData.customerID,
          typeOfOrder: "正常订单",
          companyName: "DHL",
        });
      }
    },
    onSubmitToDPD() {
      console.log("form is succefully submitted", this.formData);

      if (!this.formData.customerID) {
        this.tableData.push({
          deliveryOrder: this.formData.DOrder,
          customerID: this.formData.customerID,
          typeOfOrder: "无ID订单",
          companyName: "DPD",
        });
        alert("确定无客户ID");
      } else {
        this.tableData.push({
          deliveryOrder: this.formData.DOrder,
          customerID: this.formData.customerID,
          typeOfOrder: "正常订单",
          companyName: "DPD",
        });
      }
    },
    onSubmitToUPS() {
      console.log("form is succefully submitted", this.formData);

      if (!this.formData.customerID) {
        this.tableData.push({
          deliveryOrder: this.formData.DOrder,
          customerID: this.formData.customerID,
          typeOfOrder: "无ID订单",
          companyName: "UPS",
        });
        alert("确定无客户ID");
      } else {
        this.tableData.push({
          deliveryOrder: this.formData.DOrder,
          customerID: this.formData.customerID,
          typeOfOrder: "正常订单",
          companyName: "UPS",
        });
      }
    },
    onSubmitTohHermes() {
      console.log("form is succefully submitted", this.formData);

      if (!this.formData.customerID) {
        this.tableData.push({
          deliveryOrder: this.formData.DOrder,
          customerID: this.formData.customerID,
          typeOfOrder: "无ID订单",
          companyName: "Hermes",
        });
        alert("确定无客户ID");
      } else {
        this.tableData.push({
          deliveryOrder: this.formData.DOrder,
          customerID: this.formData.customerID,
          typeOfOrder: "正常订单",
          companyName: "Hermes",
        });
      }
    },
    onSubmitToAmz() {
      console.log("form is succefully submitted", this.formData);

      if (!this.formData.customerID) {
        this.tableData.push({
          deliveryOrder: this.formData.DOrder,
          customerID: this.formData.customerID,
          typeOfOrder: "无ID订单",
          companyName: "Amazon",
        });
        alert("确定无客户ID");
      } else {
        this.tableData.push({
          deliveryOrder: this.formData.DOrder,
          customerID: this.formData.customerID,
          typeOfOrder: "正常订单",
          companyName: "Amazon",
        });
      }
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


