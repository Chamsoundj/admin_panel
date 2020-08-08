<template>
  <div>
    <el-table
      :data="
        tableData.filter(
          data =>
            !search || data.name.toLowerCase().includes(search.toLowerCase())
        )
      "
      :default-sort="{ prop: 'date', order: 'descending' }"
      style="width: 100%"
    >
      <el-table-column label="Ifirmier" prop="name" sortable> </el-table-column>
      <el-table-column align="right">
        <template slot="header" slot-scope="scope">
          <el-input v-model="search" size="mini" placeholder="Type to search" />
        </template>
        <template slot-scope="scope">
          <el-button size="mini" @click="handleEdit(scope.$index, scope.row)"
            >Editer</el-button
          >
          <el-popconfirm
            confirmButtonText="OK"
            cancelButtonText="No, Thanks"
            icon="el-icon-info"
            iconColor="red"
            title="Are you sure to delete this?"
          >
            <el-button
              slot="reference"
              size="mini"
              type="danger"
              @click.native.prevent="deleteRow(scope.$index, tableData)"
              >Supprimer</el-button
            >
          </el-popconfirm>
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
          name: "Tom"
        },
        {
          name: "XD"
        },
        {
          name: "John"
        },
      ],
      search: ""
    };
  },
  methods: {
    handleEdit(index, row) {
      console.log(index, row);
    },
    deleteRow(index, rows) {
      rows.splice(index, 1);
    }
  }
};
</script>
