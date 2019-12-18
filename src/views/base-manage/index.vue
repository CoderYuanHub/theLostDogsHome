<template>
  <div class="super-manage">
    <div class="container">
      <div class="find">
        <el-input v-model="input" placeholder="请查询内容" style="width: 250px"></el-input>
        <el-button type="primary" icon="el-icon-search">搜索</el-button>
        <el-button type="primary" icon="el-icon-s-custom">添加管理员</el-button>
      </div>
      <el-table
        :data="tableData.filter(data => !search || data.name.toLowerCase().includes(search.toLowerCase()))"
        style="width: 100%">
        <el-table-column
          label="序号"
          type="index">
        </el-table-column>
        <el-table-column
          label="账号"
          prop="us">
        </el-table-column>
        <el-table-column
          label="姓名"
          prop="name">
        </el-table-column>
        <el-table-column
          label="地址"
          prop="address">
        </el-table-column>
        <el-table-column
          align="right">
          <template slot-scope="scope">
            <el-button
              size="mini"
              @click="handleEdit(scope.$index, scope.row)">编辑
            </el-button>
            <el-button
              size="mini"
              type="danger"
              @click="handleDelete(scope.$index, scope.row)">移除
            </el-button>
          </template>
        </el-table-column>
      </el-table>
      <div style="text-align: center">
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage"
          :page-sizes="[100, 200, 300, 400]"
          :page-size="100"
          layout="total, sizes, prev, pager, next, jumper"
          :total="412">
        </el-pagination>
      </div>
      <el-dialog
        title="修改用户密码"
        :visible.sync="dialogVisible"
        width="30%">
        <el-form ref="super" :model="tableData" label-width="80px">
          <el-form-item label="用户名">
            <el-input v-model="tableData.us"></el-input>
          </el-form-item>
          <el-form-item label="密码">
            <el-input v-model="tableData.ps"></el-input>
          </el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
            <el-button @click="dialogVisible = false">取 消</el-button>
            <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
    </div>
  </div>
</template>

<script>
    export default {
        name: 'superManager',
        data() {
            return {
                dialogVisible: false,
                input: '',
                currentPage: 4,
                tableData: [{
                    us: '123123123123',
                    ps: '111',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1518 弄'
                }, {
                    us: 'zxcscasdasda',
                    name: '王小虎',
                    ps: '111',
                    address: '上海市普陀区金沙江路 1517 弄'
                }, {
                    us: 'xcasdadawdawd',
                    name: '王小虎',
                    ps: '111',
                    address: '上海市普陀区金沙江路 1519 弄'
                }, {
                    us: 'zxcassawawc',
                    name: '王小虎',
                    ps: '111',
                    address: '上海市普陀区金沙江路 1516 弄'
                }],
                search: ''
            }
        },
        methods: {
            handleEdit(index, row) {
                this.dialogVisible = true;
                console.log(index, row);
            },
            handleDelete(index, row) {
                this.$confirm('确认移除该用户？', '确认信息', {
                    distinguishCancelAndClose: true,
                    confirmButtonText: '确定',
                    cancelButtonText: '放弃修改'
                })
                    .then(() => {
                        this.$message({
                            type: 'success',
                            message: '该用户已经移除'
                        });
                    })
                    .catch(action => {
                        this.$message({
                            type: 'info',
                            message: action === 'cancel'
                                ? '取消移除'
                                : '停留在当前页面'
                        })
                    });
            },
            handleSizeChange(val) {
                console.log(`每页 ${val} 条`);
            },
            handleCurrentChange(val) {
                console.log(`当前页: ${val}`);
            }
        }
    }
</script>

<style lang="scss" scoped>
  .container {
    padding: 20px;
  }

  .find {
    float: right;
  }
</style>
