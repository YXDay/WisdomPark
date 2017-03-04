<template>
  <div>
  <h1>智慧园区表管理系统</h1>
  <el-select v-model="value" placeholder="请选择系统">
      <el-option
        v-for="item in options"
        :label="item.label"
        :value="item.value">
      </el-option>
  </el-select>
  <el-button @click="dialogVisible = true">批量删除</el-button>
  <el-button @click="dialogTableVisible = true">创建新表</el-button>
  <el-input
    placeholder="请输入查询"
    icon="search"
    v-model="input2"
    style="width:auto;float:right">
  </el-input>
  <el-table
    :data="tableData"
    border
    style="width: 100%">
    <el-table-column
          type="selection">
        </el-table-column>
    <el-table-column
      label="分类ID">
      <template scope="scope">
        <p style="margin-left: 10px">{{ scope.row.id }}</p>
      </template>
    </el-table-column>
    <el-table-column
      label="模板名称">
      <template scope="scope">
          <p>{{ scope.row.name }}</p>
      </template>
    </el-table-column>
    <el-table-column
      label="模板路径">
      <template scope="scope">
          <p>{{ scope.row.path }}</p>
      </template>
    </el-table-column>
    <el-table-column
      label="说明">
      <template scope="scope">
          <p>{{ scope.row.description }}</p>
      </template>
    </el-table-column>
    <el-table-column
      label="创建时间">
      <template scope="scope">
          <p>{{ scope.row.date }}</p>
      </template>
    </el-table-column>
    <el-table-column label="操作">
      <template scope="scope">
        <el-button
          size="small"
          @click="handleEdit(scope.$index, scope.row)"><span class="edit">编辑</span></el-button>
        <el-button
          size="small"
          type="danger"
          @click="handleDelete(scope.$index, scope.row)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
  <div class="block">
      <el-pagination
        :current-page="1"
        :page-sizes="[100, 200, 300, 400]"
        :page-size="100"
        layout="total, sizes, prev, pager, next, jumper"
        :total="400">
      </el-pagination>
    </div>
    <el-dialog title="提示" v-model="dialogVisible" size="tiny">
      <span>确认删除?</span>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="deleteData">确 定</el-button>
      </span>
    </el-dialog>
    <el-dialog title="请输入" v-model="dialogTableVisible">
        <el-input
          type="textarea"
          :rows="2"
          placeholder="请输入内容"
          v-model="textarea">
        </el-input>
    </el-dialog>
  </div>
</template>

<script>
  import 'element-ui/lib/theme-default/index.css'
  export default {
    data() {
      return {
        tableData: [{
          id: '1',
          name: '模板名称1',
          path: '模板路径1',
          description: '模板说明1',
          date: '创建时间1'
        },{
          id: '2',
          name: '模板名称2',
          path: '模板路径2',
          description: '模板说明2',
          date: '创建时间2'
        },{
          id: '3',
          name: '模板名称3',
          path: '模板路径3',
          description: '模板说明3',
          date: '创建时间3'
        },{
          id: '4',
          name: '模板名称4',
          path: '模板路径4',
          description: '模板说明4',
          date: '创建时间4'
        },{
          id: '5',
          name: '模板名称5',
          path: '模板路径5',
          description: '模板说明5',
          date: '创建时间5'
        }
        ],
        options: [{
                  value: '选项1',
                  label: '安防系统'
                }, {
                  value: '选项2',
                  label: '地信系统'
                }, {
                  value: '选项3',
                  label: '环境系统'
                }, {
                  value: '选项4',
                  label: '能源系统'
                }, {
                  value: '选项5',
                  label: '物流系统'
                }],
                value: '',
                input2: '',
                dialogVisible: false,
                dialogTableVisible: false,
                textarea:''
      };
    },
    methods: {
      handleEdit(index, row) {
        console.log(index, row);
        // 这里好大一个坑啊,万恶的vue 绑定this哈哈哈
        if ($($('tr')[index+1]).find('.edit').text() === '编辑' ) {
            $($('tr')[index+1]).find('.edit').text('完成');
        }
        else {
            this.$message({
                      message: '修改成功',
                      type: 'success'
            });
            $($('tr')[index+1]).find('.edit').text('编辑');
        }
        $($('tr')[index+1]).find('p').each((index,element) => {
          // $(this).attr('contentEditable', true);
          // console.log($(this));
          if ($(element).attr('contentEditable')) {
            $(element).attr('contentEditable', false);
          }
          else {
            $(element).attr('contentEditable', true);
          }
        });
      },
      handleDelete(index, row) {
        console.log(index, row);
        this.dialogVisible = true;
      },
      deleteData() {
        this.dialogVisible = false;
        this.$message({
                  message: '删除成功',
                  type: 'success'
        });
      }
    }
  }
</script>