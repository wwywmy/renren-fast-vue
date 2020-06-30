<template>
  <div class="mod-user">
    <el-form :model="dataForm" label-width="160px" label-position="right">
      <el-row>
        <el-col :span="6">
          <el-form-item label="tableName">
            <el-select v-model="dataForm.tableName" placeholder="表名" @change="tableSelectChange()">
              <el-option
                v-for="item in tableOptions"
                :key="item.tableName"
                :label="item.tableName"
                :value="item.tableName"
              ></el-option>
            </el-select>
          </el-form-item>
        </el-col>
        <el-col :span="6">
          <el-form-item label="tableShortName">
            <el-input v-model="tableInfo.tableShortName" :disabled="true"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="6">
          <el-form-item label="tablePrefix">
            <el-input v-model="tableInfo.tablePrefix" :disabled="true"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="6">
          <el-form-item label="tableComment">
            <el-input v-model="tableInfo.tableComment" :disabled="true"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="6">
          <el-form-item label="entityName">
            <el-input v-model="tableInfo.entityName" :disabled="true"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="6">
          <el-form-item label="restSegment">
            <el-input v-model="tableInfo.restSegment" :disabled="true"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="3">
          <el-form-item label="BigDecimal">
            <el-switch
              v-model="tableInfo.includeBigDecimal"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="Long">
            <el-switch
              v-model="tableInfo.includeLong"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="Date">
            <el-switch
              v-model="tableInfo.includeDate"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="Status">
            <el-switch
              v-model="tableInfo.includeStatus"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="CompanyShortName">
            <el-switch
              v-model="tableInfo.includeCompanyShortName"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="3">
          <el-form-item label="TenantId">
            <el-switch
              v-model="tableInfo.includeTenantId"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="TenantOne2One">
            <el-switch
              v-model="tableInfo.includeTenantOne2One"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="TenantOne2Many">
            <el-switch
              v-model="tableInfo.includeTenantOne2Many"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="ModuleId">
            <el-switch
              v-model="tableInfo.includeModuleId"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="ModuleOne2One">
            <el-switch
              v-model="tableInfo.includeModuleOne2One"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="ModuleOne2Many">
            <el-switch
              v-model="tableInfo.includeModuleOne2Many"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="3">
          <el-form-item label="SingleUpdatable">
            <el-switch
              v-model="tableInfo.includeSingleUpdatable"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="BatchUpdatable">
            <el-switch
              v-model="tableInfo.includeBatchUpdatable"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="NotNullabe">
            <el-switch
              v-model="tableInfo.includeNotNullabe"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="ParentId">
            <el-switch
              v-model="tableInfo.includeParentId"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="Aggregation">
            <el-switch
              v-model="tableInfo.includeAggregation"
              active-color="#13ce66"
              inactive-color="#ff4949"
              disabled
            ></el-switch>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="24">
          <el-form-item>
            <el-button @click="create()">生成</el-button>
          </el-form-item>
        </el-col>
      </el-row>
    </el-form>
    <el-table
      :data="dataList"
      border
      v-loading="dataListLoading"
      @selection-change="selectionChangeHandle"
      style="width: 100%;"
    >
      <el-table-column prop="columnName" header-align="center" width="180" label="columnName"></el-table-column>
      <el-table-column prop="isNullable" header-align="center" align="center" label="isNullable">
        <template slot-scope="scope">
          <el-switch
            v-model="scope.row.isNullable"
            active-value="YES"
            inactive-value="NO"
            active-color="#13ce66"
            inactive-color="#ff4949"
          ></el-switch>
        </template>
      </el-table-column>
      <el-table-column
        prop="dataType"
        header-align="center"
        align="center"
        label="dataType"
        :formatter="dataTypeFormatter"
      ></el-table-column>
      <el-table-column prop="columnKey" header-align="center" align="center" label="columnKey">
        <template slot-scope="scope">
          <el-tag v-if="scope.row.columnKey === 'PRI'" size="small" type="danger">PRI</el-tag>
          <el-tag v-if="scope.row.columnKey === 'UNI'" size="small" type="warning">UNI</el-tag>
          <el-tag v-if="scope.row.columnKey === 'MUL'" size="small" type="success">MUL</el-tag>
        </template>
      </el-table-column>
      <el-table-column prop="extra" header-align="center" align="center" label="extra">
        <template slot-scope="scope">
          <el-tag
            v-if="scope.row.extra === 'auto_increment'"
            size="small"
            type="danger"
          >auto_increment</el-tag>
        </template>
      </el-table-column>

      <el-table-column prop="columnComment" header-align="center" width="320" label="columnComment"></el-table-column>
      <el-table-column fixed="right" header-align="center" align="center" width="100" label="操作">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click="addOrUpdateHandle(scope.row)">修改</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      @size-change="sizeChangeHandle"
      @current-change="currentChangeHandle"
      :current-page="pageIndex"
      :page-sizes="[10, 20, 50, 100]"
      :page-size="pageSize"
      :total="totalPage"
      layout="total, sizes, prev, pager, next, jumper"
    ></el-pagination>
    <!-- 弹窗, 新增 / 修改 -->
    <add-or-update v-if="addOrUpdateVisible" ref="addOrUpdate" @refreshDataList="getDataList"></add-or-update>
  </div>
</template>

<script>
import AddOrUpdate from "./field-add-or-update";
export default {
  data() {
    return {
      dataForm: {
        tableName: ""
      },
      tableInfo: {
        tableName: "",
        tableComment: "",
        tableShortName: ""
      },
      tableOptions: [],
      dataList: [],
      pageIndex: 1,
      pageSize: 100,
      totalPage: 0,
      dataListLoading: false,
      dataListSelections: [],
      addOrUpdateVisible: false
    };
  },
  components: {
    AddOrUpdate
  },
  created() {
    this.getTableList();
  },
  activated() {
    //this.getDataList();
  },
  methods: {
    tableSelectChange() {
      this.getDataList();
      this.getTableInfo();
    },
    // 获取数据列表
    getTableList() {
      this.dataListLoading = true;
      this.$http({
        url: this.$http.adornUrl("/table/list"),
        method: "get",
        params: this.$http.adornParams({})
      }).then(({ data }) => {
        if (data && data.code === 0) {
          //this.dataList = data.page.list;
          //this.totalPage = data.page.totalCount;
          //this.tableOptions = data.page.list;
          this.tableOptions = data.data;
          this.dataForm.tableName = this.tableOptions[0].tableName;
          this.tableSelectChange();
          //this.tableInfo = this.tableOptions[0];
        } else {
          //this.dataList = [];
          //this.totalPage = 0;
          this.tableOptions = [];
        }
        this.dataListLoading = false;
      });
    },
    getTableInfo() {
      this.dataListLoading = true;
      this.$http({
        url: this.$http.adornUrl("/table/" + this.dataForm.tableName),
        method: "get",
        params: this.$http.adornParams({})
      }).then(({ data }) => {
        if (data && data.code === 0) {
          //this.dataList = data.page.list;
          //this.totalPage = data.page.totalCount;
          this.tableInfo = data.data;
        } else {
          //this.dataList = [];
          //this.totalPage = 0;
        }
        this.dataListLoading = false;
      });
    },
    // 获取数据列表
    getDataList() {
      this.dataListLoading = true;
      this.$http({
        url: this.$http.adornUrl("/table/" + this.dataForm.tableName),
        method: "get",
        params: this.$http.adornParams({
          page: this.pageIndex,
          limit: this.pageSize,
          tableName: this.dataForm.tableName
        })
      }).then(({ data }) => {
        if (data && data.code === 0) {
          this.dataList = data.data.columnList;
          this.totalPage = data.data.columnList.length;
        } else {
          this.dataList = [];
          this.totalPage = 0;
        }
        this.dataListLoading = false;
      });
    },
    dataTypeFormatter(row, column, cellValue, index) {
      if (cellValue === "varchar") {
        return cellValue + "(" + row.characterMaximumLength + ")";
      } else if (
        cellValue === "bigint" ||
        cellValue === "int" ||
        cellValue === "tinyint"
      ) {
        return cellValue + "(" + (row.numericPrecision + 1) + ")";
      } else if (cellValue === "decimal") {
        return (
          cellValue + "(" + row.numericPrecision + "," + row.numericScale + ")"
        );
      }

      return cellValue;
    },
    // 每页数
    sizeChangeHandle(val) {
      this.pageSize = val;
      this.pageIndex = 1;
      this.getDataList();
    },
    // 当前页
    currentChangeHandle(val) {
      this.pageIndex = val;
      this.getDataList();
    },
    // 多选
    selectionChangeHandle(val) {
      this.dataListSelections = val;
    },
    // 新增 / 修改
    addOrUpdateHandle(row) {
      this.addOrUpdateVisible = true;
      this.$nextTick(() => {
        this.$refs.addOrUpdate.init(row);
      });
    },
    create() {
      this.dataListLoading = true;
      this.$http({
        url: this.$http.adornUrl("/table/create/" + this.dataForm.tableName),
        method: "post",
        params: this.$http.adornParams({})
      }).then(({ data }) => {
        if (data && data.code === 0) {
          //this.dataList = data.data.columnList;
          //this.totalPage = data.data.columnList.length;
          this.$message({
            message: "操作成功",
            type: "success",
            duration: 1500,
            onClose: () => {}
          });
        } else {
          //this.dataList = [];
          //this.totalPage = 0;
          this.$message.error(data.msg);
        }
        this.dataListLoading = false;
      });
    }
  }
};
</script>
