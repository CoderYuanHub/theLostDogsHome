<template>
  <div class="super-manage">
    <div class="container">
      <div class="find">
        <el-input v-model="input" placeholder="请查询内容" style="width: 250px"></el-input>
        <el-button type="primary" icon="el-icon-search">搜索</el-button>
        <el-button type="primary" icon="el-icon-s-custom" @click="addPet">添加宠物</el-button>
      </div>
      <el-table
        :data="tableData.filter(data => !search || data.name.toLowerCase().includes(search.toLowerCase()))"
        style="width: 100%">
        <el-table-column
          label="序号"
          type="index">
        </el-table-column>
        <el-table-column
          label="名称"
          prop="name">
        </el-table-column>
        <el-table-column
          label="照片">
          <template   slot-scope="url">
<!--            <img :src="url"  min-width="70" height="70" />-->
          </template>
        </el-table-column>
        <el-table-column
          label="类别"
          prop="address">
        </el-table-column>
        <el-table-column
          label="注册时间"
          prop="us">
        </el-table-column>
        <el-table-column
          label="宠物情况"
          prop="us">
        </el-table-column>
        <el-table-column
          align="right">
          <template slot-scope="scope">
            <el-button
              size="mini"
              @click="handleEdit(scope.$index, scope.row)">详情
            </el-button>
            <el-button
              size="mini"
              type="success"
              @click="handleDelete(scope.$index, scope.row)">领养
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
        title="新增宠物"
        :visible.sync="addDialog"
        width="30%"
        :before-close="handleClose">
        <el-form ref="pet" :model="pet" label-width="80px">
          <el-form-item label="宠物名称">
            <el-input v-model="pet.name"></el-input>
          </el-form-item>
          <el-form-item label="宠物类型">
            <el-select v-model="value" placeholder="请选择">
              <el-option
                v-for="item in petType"
                :key="item.value"
                :label="item.label"
                :value="item.value">
              </el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="宠物情况">
            <el-input v-model="pet.name"></el-input>
          </el-form-item>
          <el-form-item label="宠物照片">
            <el-upload
              action="http://localhost:9528/"
              list-type="picture-card"
              :on-preview="handlePictureCardPreview"
              :on-remove="handleRemove"
              :limit=3>
              <i class="el-icon-plus"></i>
            </el-upload>
            <el-dialog :visible.sync="dialogPhotoes">
              <img width="100%" :src="dialogImageUrl" alt="">
            </el-dialog>
          </el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
      <el-button @click="addDialog = false">取 消</el-button>
      <el-button type="primary" @click="addDialog = false">确 定</el-button>
        </span>
      </el-dialog>
    </div>
  </div>
</template>

<script>
	export default {
		name: 'basePet',
		data() {
			return {
        addDialog: false,
				input: '',
		    pet:{},
        petType:[
              {
            value: '选项1',
            label: '黄金糕'
          }, {
            value: '选项2',
            label: '双皮奶'
          }, {
            value: '选项3',
            label: '蚵仔煎'
          }, {
            value: '选项4',
            label: '龙须面'
          }, {
            value: '选项5',
            label: '北京烤鸭'
          }
        ],
        url: 'https://fuss10.elemecdn.com/1/8e/aeffeb4de74e2fde4bd74fc7b4486jpeg.jpeg',
		    value:'',
				currentPage: 4,
        dialogImageUrl: '',
        dialogPhotoes: false,
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
				this.addDialog = true;
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
			},
      handleClose(done) {
        this.$confirm('确认关闭？')
          .then(_ => {
            done();
          })
          .catch(_ => {});
      },
		  addPet() {
				this.addDialog = true;
      },
      handleRemove(file, fileList) {
        console.log(file, fileList);
      },
      handlePictureCardPreview(file) {
        this.dialogImageUrl = file.url;
        this.dialogVisible = true;
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
