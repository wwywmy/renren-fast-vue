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
      <el-tabs tab-position="left">
        <el-tab-pane label="代码">
          <el-form-item label="propertyName" prop="propertyName">
            <el-input v-model="dataForm.propertyName"></el-input>
          </el-form-item>
          <el-form-item label="propertyType" prop="propertyType">
            <el-select v-model="dataForm.propertyType" placeholder>
              <el-option
                v-for="item in propertyTypeOptions"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              ></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="propertyComment" prop="propertyComment">
            <el-input v-model="dataForm.propertyComment"></el-input>
          </el-form-item>
          <el-form-item label="propertySelect" prop="propertySelect">
            <el-switch
              v-model="dataForm.propertySelect"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </el-form-item>
          <el-form-item
            label="propertyOptionList"
            prop="propertyOptionList"
            :v-if="dataForm.propertySelect"
          >
            <el-input v-model="dataForm.propertyOptionList" :disabled="true"></el-input>
          </el-form-item>          
        </el-tab-pane>
        <el-tab-pane label="配置">
          <el-form-item label="queryable" prop="queryable">
            <el-switch
              v-model="dataForm.queryable"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </el-form-item>
          <el-form-item label="likeable" prop="likeable">
            <el-switch
              v-model="dataForm.likeable"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </el-form-item>
          <el-form-item label="addable" prop="addable">
            <el-switch
              v-model="dataForm.addable"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </el-form-item>
          <el-form-item label="updatable" prop="updatable">
            <el-switch
              v-model="dataForm.updatable"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </el-form-item>
          <el-form-item label="selectable" prop="selectable">
            <el-switch
              v-model="dataForm.selectable"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </el-form-item>
          <el-form-item label="addableOrUpdatable" prop="addableOrUpdatable">
            <el-switch
              v-model="dataForm.addableOrUpdatable"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </el-form-item>
          <el-form-item label="defaultAddValue" prop="defaultAddValue">
            <el-input v-model="dataForm.defaultAddValue" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="defaultUpdateValue" prop="defaultUpdateValue">
            <el-input v-model="dataForm.defaultUpdateValue" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="singleUpdatable" prop="singleUpdatable">
            <el-switch
              v-model="dataForm.singleUpdatable"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </el-form-item>
          <el-form-item label="batchUpdatable" prop="batchUpdatable">
            <el-switch
              v-model="dataForm.batchUpdatable"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </el-form-item>
          <el-form-item label="viewable" prop="viewable">
            <el-switch
              v-model="dataForm.viewable"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </el-form-item>
          <el-form-item label="detailable" prop="detailable">
            <el-switch
              v-model="dataForm.detailable"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </el-form-item>
          <el-form-item label="ynSelectable" prop="ynSelectable">
            <el-switch
              v-model="dataForm.ynSelectable"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </el-form-item>
          <el-form-item label="refEntityName" prop="refEntityName">
            <el-input v-model="dataForm.refEntityName" ></el-input>
          </el-form-item>
        </el-tab-pane>
        <el-tab-pane label="Grid显示">
          <el-form-item label="gridWidthAuto" prop="gridWidthAuto">
            <el-input v-model="dataForm.gridWidthAuto" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="gridWidth" prop="gridWidth">
            <el-input v-model="dataForm.gridWidth" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="gridAlign" prop="gridAlign">
            <el-input v-model="dataForm.gridAlign" :disabled="true"></el-input>
          </el-form-item>
        </el-tab-pane>
        <el-tab-pane label="数据库">
          <el-form-item label="tableSchema" prop="tableSchema">
            <el-input v-model="dataForm.tableSchema" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="tableName" prop="tableName">
            <el-input v-model="dataForm.tableName" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="columnName" prop="columnName">
            <el-input v-model="dataForm.columnName" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="isNullable" prop="isNullable">
            <el-input v-model="dataForm.isNullable" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="dataType" prop="dataType">
            <el-input v-model="dataForm.dataType" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="characterMaximumLength" prop="characterMaximumLength">
            <el-input v-model="dataForm.characterMaximumLength" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="characterOctetLength" prop="characterOctetLength">
            <el-input v-model="dataForm.characterOctetLength" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="numericPrecision" prop="numericPrecision">
            <el-input v-model="dataForm.numericPrecision" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="numericScale" prop="numericScale">
            <el-input v-model="dataForm.numericScale" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="columnKey" prop="columnKey">
            <el-input v-model="dataForm.columnKey" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="extra" prop="extra">
            <el-input v-model="dataForm.extra" :disabled="true"></el-input>
          </el-form-item>
          <el-form-item label="columnComment" prop="columnComment">
            <el-input v-model="dataForm.columnComment" :disabled="true"></el-input>
          </el-form-item>
        </el-tab-pane>
      </el-tabs>
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
      propertyTypeOptions: [
        { value: "Byte", label: "Byte" },
        { value: "Short", label: "Short" },
        { value: "Integer", label: "Integer" },
        { value: "Long", label: "Long" },
        { value: "Float", label: "Float" },
        { value: "Double", label: "Double" },
        { value: "BigDecimal", label: "BigDecimal" },
        { value: "String", label: "String" },
        { value: "byte []", label: "byte []" },
        { value: "Date", label: "Date" },
        { value: "Time", label: "Time" }
      ],
      visible: false,
      roleList: [],
      dataForm: {},
      dataRule: {}
    };
  },
  methods: {
    init(row) {
      //this.dataForm.tableName = row.tableName || "";
      //this.dataForm.columnName = row.columnName || "";

      this.dataForm = Object.assign({}, row);

      this.visible = true;
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
