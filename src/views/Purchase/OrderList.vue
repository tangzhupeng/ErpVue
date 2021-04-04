<template>
    <div>
      <!--新增购货订单按钮-->
      <el-button type="primary" style="margin: 10px">+新增购货订单</el-button>
      <!--高级筛选按钮-->
      <el-button @click="drawer = true" type="primary" style="margin-left: 6px;" icon="el-icon-search">
      高级筛选
      </el-button>
<!--      下拉框-->
      <el-select v-model="value" style="margin-left: 16px;" filterable placeholder="请选择">
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value">
        </el-option>
      </el-select>
<!--      搜索框-->
      <el-input
        placeholder="请输入内容"
        v-model="input"
        style="margin-left: 16px;width: 300px"
        clearable>
      </el-input>
      <el-button type="primary">搜索</el-button>
      <!--页头切换-->
      <el-tabs v-model="activeName" @tab-click="handleClick" style="margin: 10px">
        <!--采购订单页头-->
        <el-tab-pane label="采购订单" name="first">

          <!--表格-->
          <el-table
            :data="tableData"
            style="width: 100%;"
            :summary-method="getSummaries"
            show-summary
            height="250">
            <el-table-column
              fixed
              prop="date"
              label="订单日期"
              width="150">
            </el-table-column>
            <el-table-column
              fixed
              prop="name"
              label="单据编号"
              width="120">
            </el-table-column>
            <el-table-column
              prop="province"
              label="业务类别"
              width="120">
            </el-table-column>
            <el-table-column
              prop="city"
              label="供应商"
              width="120">
            </el-table-column>
            <el-table-column
              prop="address"
              label="采购人员"
              width="300">
            </el-table-column>
            <el-table-column
              prop="zip"
              label="仓库"
              width="120">
            </el-table-column>
            <el-table-column
              prop="zip"
              label="关联入库单"
              width="120">
            </el-table-column>
            <el-table-column
              prop="zip"
              label="购货金额"
              width="120">
            </el-table-column>
            <el-table-column
            prop="name"
            label="订单状态"
            width="120">
          </el-table-column>
            <el-table-column
              prop="province"
              label="审批状态"
              width="120">
            </el-table-column>
            <el-table-column
              prop="city"
              label="审批人"
              width="120">
            </el-table-column>
            <el-table-column
              prop="address"
              label="入库状态"
              width="300">
            </el-table-column>
          </el-table>

          <!--分页-->
          <div class="pager">
            <el-pagination
              background
              @size-change="handleSizeChange"
              @current-change="handleCurrentChange"
              :current-page="currentPage"
              :page-sizes="[5, 10, 20, 50]"
              :page-size="100"
              layout="total, sizes, prev, pager, next, jumper"
              :total="400"
            >
            </el-pagination>
          </div>

          <!--抽屉弹框-->
          <el-drawer
            title="我是标题"
            :visible.sync="drawer"
            :with-header="false">

            <div style="margin: 10px">
            单据编号：<el-input
            placeholder="请输入内容"
            v-model="input"
            style="margin-left: 16px;width: 300px"
            clearable>
          </el-input>
            </div>

            <div style="margin: 10px">
              单据日期：
              <el-date-picker
                v-model="value1"
                type="daterange"
                align="right"
                unlink-panels
                range-separator="至"
                start-placeholder="开始日期"
                end-placeholder="结束日期"
                :picker-options="pickerOptions">
              </el-date-picker>
            </div>

            <el-button type="primary" style="margin: 10px" icon="el-icon-search">搜索</el-button>
            <el-button type="primary" style="margin: 10px" icon="el-icon-refresh">重置</el-button>
          </el-drawer>
        </el-tab-pane>

        <!--采购入库页头-->
        <el-tab-pane label="采购入库" name="second">
          采购入库
        </el-tab-pane>

        <!--采购退货页头-->
        <el-tab-pane label="采购退货" name="third">
          采购退货
        </el-tab-pane>

      </el-tabs>

    </div>
</template>

<script>
export default {
  name: 'OrderList',
  data() {
    return {
      activeName: 'first',// 页头切换
      drawer: false,// 筛选抽屉
      currentPage: 5,
      // 分页
      handleSizeChange(val) {
        console.log(`每页 ${val} 条`);
      },
      handleCurrentChange(val) {
        console.log(`当前页: ${val}`);
      },
      // 表格
      tableData: [{
        date: '2016-05-03',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }, {
        date: '2016-05-02',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }, {
        date: '2016-05-04',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }, {
        date: '2016-05-01',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }, {
        date: '2016-05-08',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }, {
        date: '2016-05-06',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }, {
        date: '2016-05-07',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }],
      // 下拉框
      options: [{
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
      }],
      value: '',
      value1: '',
      //下拉框
      input: '',
      // 日期选择
      pickerOptions: {
        shortcuts: [{
          text: '最近一周',
          onClick(picker) {
            const end = new Date();
            const start = new Date();
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
            picker.$emit('pick', [start, end]);
          }
        }, {
          text: '最近一个月',
          onClick(picker) {
            const end = new Date();
            const start = new Date();
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
            picker.$emit('pick', [start, end]);
          }
        }, {
          text: '最近三个月',
          onClick(picker) {
            const end = new Date();
            const start = new Date();
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
            picker.$emit('pick', [start, end]);
          }
        }]
      },
    }
  },
  methods: {
    handleClick(tab, event) {
      console.log(tab, event)
    },
    getSummaries(param) {
      const { columns, data } = param;
      const sums = [];
      columns.forEach((column, index) => {
        if (index === 0) {
          sums[index] = '合计:';
          return;
        }
        const values = data.map(item => Number(item[column.property]));
        if (!values.every(value => isNaN(value))) {
          sums[index] = values.reduce((prev, curr) => {
            const value = Number(curr);
            if (!isNaN(value)) {
              return prev + curr;
            } else {
              return prev;
            }
          }, 0);
          sums[index] += ' 元';
        } else {
          sums[index] = '';
        }
      });

      return sums;
    }
  }
}
</script>

<style scoped>
  .pager{
    text-align: center;
    margin-top: 20px;
  }
</style>
