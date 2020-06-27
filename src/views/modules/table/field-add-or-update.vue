<template>
  <el-dialog
    :title="!dataForm.columnName ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible"
  >
    <el-form
      :model="dataForm"
      :rules="dataRule"
      ref="dataForm"
      @keyup.enter.native="dataFormSubmit()"
      label-width="140px"
      label-position="right"
    >
      <el-form-item label="tableSchema" prop="tableSchema">
        <el-input v-model="dataForm.tableSchema" :disabled="true"></el-input>
      </el-form-item>
      <el-form-item label="tableName" prop="tableName">
        <el-input v-model="dataForm.tableName" :disabled="true"></el-input>
      </el-form-item>
      <el-form-item label="columnName" prop="columnName">
        <el-input v-model="dataForm.columnName" :disabled="true"></el-input>
      </el-form-item>

      <el-form-item label="propertyName" prop="propertyName">
        <el-input v-model="dataForm.propertyName"></el-input>
      </el-form-item>
      <el-form-item label="propertyType" prop="propertyType">
        <el-input v-model="dataForm.propertyType"></el-input>
      </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="visible = false">取消</el-button>
      <el-button type="primary" @click="dataFormSubmit()">确定</el-button>
    </span>
  </el-dialog>
</template>

<script>
import { isEmail, isMobile } from "@/utils/validate";
export default {
  data() {
    return {
      visible: false,
      roleList: [],
      dataForm: {
        tableSchema: "",
        tableName: "",
        columnName: "",
        isNullable: "",

        propertyName: "",
        propertyType: ""
      },
      dataRule: {}
    };
  },
  methods: {
    init(tableName, columnName) {
      this.dataForm.tableName = tableName || "";
      this.dataForm.columnName = columnName || "";

      this.visible = true;
      this.$nextTick(() => {
        this.$refs["dataForm"].resetFields();
      });
      this.$http({
        url: this.$http.adornUrl(
          "/table/field/" +
            this.dataForm.tableName +
            "/" +
            this.dataForm.columnName
        ),
        method: "get",
        params: this.$http.adornParams()
      }).then(({ data }) => {
        if (data && data.code === 0) {
          this.dataForm.tableSchema = data.tableField.tableSchema;
          this.dataForm.tableName = data.tableField.tableName;
          this.dataForm.columnName = data.tableField.columnName;
          this.dataForm.isNullable = data.tableField.isNullable;

          this.dataForm.propertyName = data.tableField.propertyName;
          this.dataForm.propertyType = data.tableField.propertyType;
        }
      });
    },
    // 表单提交
    dataFormSubmit() {
      this.$refs["dataForm"].validate(valid => {
        if (valid) {
          this.$http({
            url: this.$http.adornUrl(
              `/sys/user/${!this.dataForm.columnName ? "save" : "update"}`
            ),
            method: "post",
            data: this.$http.adornData({})
          }).then(({ data }) => {
            if (data && data.code === 0) {
              this.$message({
                message: "操作成功",
                type: "success",
                duration: 1500,
                onClose: () => {
                  this.visible = false;
                  this.$emit("refreshDataList");
                }
              });
            } else {
              this.$message.error(data.msg);
            }
          });
        }
      });
    }
  }
};
</script>
