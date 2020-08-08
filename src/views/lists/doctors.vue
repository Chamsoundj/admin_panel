<template>
  <div>
    <el-button
      style="margin: 10px; float:right"
      size="medium"
      type="primary"
      icon="el-icon-edit"
      @click="handleCreate"
    >
      Add
    </el-button>
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
      <el-table-column label="Medecin" prop="name" sortable> </el-table-column>
      <el-table-column label="Grade" prop="grade" sortable> </el-table-column>
      <el-table-column align="right">
        <template slot="header" slot-scope="scope">
          <el-input v-model="search" size="mini" placeholder="Type to search" />
        </template>
        <template slot-scope="scope">
          <el-button size="mini" type="success" @click="handleEdit(scope.$index, scope.row)"
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
    <div>
      <el-dialog
        :title="textMap[dialogStatus]"
        :visible.sync="dialogFormVisible"
      >
        <el-form
          ref="dataForm"
          :rules="rules"
          :model="temp"
          label-position="left"
          label-width="70px"
          style="width: 400px; margin-left:50px;"
        >
          <el-form-item label="Type" prop="type">
            <el-select
              v-model="temp.type"
              class="filter-item"
              placeholder="Please select"
            >
              <el-option
                v-for="item in calendarTypeOptions"
                :key="item.key"
                :label="item.display_name"
                :value="item.key"
              />
            </el-select>
          </el-form-item>
          <el-form-item label="Date" prop="timestamp">
            <el-date-picker
              v-model="temp.timestamp"
              type="datetime"
              placeholder="Please pick a date"
            />
          </el-form-item>
          <el-form-item label="Title" prop="title">
            <el-input v-model="temp.title" />
          </el-form-item>
          <el-form-item label="Status">
            <el-select
              v-model="temp.status"
              class="filter-item"
              placeholder="Please select"
            >
              <el-option
                v-for="item in statusOptions"
                :key="item"
                :label="item"
                :value="item"
              />
            </el-select>
          </el-form-item>
          <el-form-item label="Imp">
            <el-rate
              v-model="temp.importance"
              :colors="['#99A9BF', '#F7BA2A', '#FF9900']"
              :max="3"
              style="margin-top:8px;"
            />
          </el-form-item>
          <el-form-item label="Remark">
            <el-input
              v-model="temp.remark"
              :autosize="{ minRows: 2, maxRows: 4 }"
              type="textarea"
              placeholder="Please input"
            />
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button @click="dialogFormVisible = false">
            Cancel
          </el-button>
          <el-button
            type="primary"
            @click="dialogStatus === 'create' ? createData() : updateData()"
          >
            Confirm
          </el-button>
        </div>
      </el-dialog>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        {
          name: "Tom",
          grade: "Chef de service"
        },
        {
          name: "XD",
          grade: "Externe"
        },
        {
          name: "John",
          grade: "Interne"
        }
      ],
      search: "",
      temp: {
        id: undefined,
        importance: 1,
        remark: "",
        timestamp: new Date(),
        title: "",
        type: "",
        status: "published"
      },
      dialogFormVisible: false,
      dialogStatus: "",
      textMap: {
        update: "Edit",
        create: "Create"
      },
      dialogPvVisible: false,
      pvData: [],
      rules: {
        type: [
          { required: true, message: "type is required", trigger: "change" }
        ],
        timestamp: [
          {
            type: "date",
            required: true,
            message: "timestamp is required",
            trigger: "change"
          }
        ],
        title: [
          { required: true, message: "title is required", trigger: "blur" }
        ]
      },
      downloadLoading: false
    };
  },

  methods: {
    handleEdit(index, row) {
      console.log(index, row);
    },
    deleteRow(index, rows) {
      rows.splice(index, 1);
    },

    resetTemp() {
      this.temp = {
        id: undefined,
        importance: 1,
        remark: "",
        timestamp: new Date(),
        title: "",
        status: "published",
        type: ""
      };
    },
    handleCreate() {
      this.resetTemp();
      this.dialogStatus = "create";
      this.dialogFormVisible = true;
      this.$nextTick(() => {
        this.$refs["dataForm"].clearValidate();
      });
    },
    createData() {
      this.$refs["dataForm"].validate(valid => {
        if (valid) {
          this.temp.id = parseInt(Math.random() * 100) + 1024; // mock a id
          this.temp.author = "vue-element-admin";
          createArticle(this.temp).then(() => {
            this.list.unshift(this.temp);
            this.dialogFormVisible = false;
            this.$notify({
              title: "Success",
              message: "Created Successfully",
              type: "success",
              duration: 2000
            });
          });
        }
      });
    }
  }
};
</script>
