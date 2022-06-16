<template>
  <div>
    <el-button @click="resetDateFilter">清除日期过滤器</el-button>
    <el-button @click="clearFilter">清除所有过滤器</el-button>
    <el-table ref="filterTable" :data="tableData" style="width: 100%">
      <el-table-column
        prop="date"
        label="日期"
        sortable
        width="180"
        column-key="date"
        :filters="[
          { text: '2016-05-01', value: '2016-05-01' },
          { text: '2016-05-02', value: '2016-05-02' },
          { text: '2016-05-03', value: '2016-05-03' },
          { text: '2016-05-04', value: '2016-05-04' },
        ]"
        :filter-method="filterHandler"
      >
      </el-table-column>
      <el-table-column prop="name" label="姓名" width="180"> </el-table-column>

      <el-table-column prop="fault" label="错题" :formatter="formatter">
      </el-table-column>
      <el-table-column
        prop="teachers"
        label="助教"
        width="100"
        :filters="[
          { text: '家', value: '家' },
          { text: '公司', value: '公司' },
        ]"
        :filter-method="filterteachers"
        filter-placement="bottom-end"
      >
        <template slot-scope="scope">
          <el-select v-model="value" placeholder="请选择">
            <el-option
              v-for="item in scope.row.teachers"
              :key="item.id"
              :label="item.name"
              :value="item.id"
            >
            </el-option>
          </el-select>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        {
          date: "2016-05-02",
          name: "张",
          fualt: "错题1",
          teachers: [{ id: 1, name: "chengjingyu" }],
        },
        {
          date: "2016-05-04",
          name: "李",
          fualt: "错题2",
          teachers: [{ id: 1, name: "lurongkun" }],
        },
        {
          date: "2016-05-01",
          name: "陆",
          fualt: "错题3",
          teachers: [{ id: 1, name: "lurongkun" }],
        },
        {
          date: "2016-05-03",
          name: "陈",
          fualt: "错题4",
          teachers: [{ id: 1, name: "lurongkun" }],
        },
      ],
    };
  },
  methods: {
    resetDateFilter() {
      this.$refs.filterTable.clearFilter("date");
    },
    clearFilter() {
      this.$refs.filterTable.clearFilter();
    },
    formatter(row) {
      return row.fualt;
    },
    filterteachers(value, row) {
      return row.teachers === value;
    },
    filterHandler(value, row, column) {
      const property = column["property"];
      return row[property] === value;
    },
  },
};
</script>
