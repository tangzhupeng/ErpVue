<template>
  <div class="salesOrder">
    <div class="top">
      <div class="top_left">
        <span>采购订单</span>
          <!--          <el-button type="primary" @click="editForm(s.row),formVissble=true" icon="el-icon-edit" round align="center">编辑</el-button>-->
      </div>
      <div class="top_right">
          <el-button type="round" @click="openGoods" style="width: 100%;height: 20px;margin-left: 20px" icon="el-icon-shopping-cart-full">提交审批</el-button>
      </div>
    </div>

    <el-card class="box-card">
      <div class="head">
        <el-form :inline="true" size="mini" label-width="100px"  :model="ruleForm" :rules="rules" ref="ruleForm" class="demo-ruleForm">
          <el-form-item label="编号" prop="name">
            <el-input v-model="ruleForm.name" style="width: 200px"></el-input>
          </el-form-item>
          <el-form-item label="单据日期" prop="name">
            <el-date-picker
                style="width: 200px"
                v-model="value1"
                type="date"
                placeholder="选择日期">
            </el-date-picker>
          </el-form-item>
          <el-form-item label="交货日期" prop="name">
            <el-date-picker
                style="width: 200px"
                v-model="value2"
                type="date"
                placeholder="选择日期">
            </el-date-picker>
          </el-form-item>
          <el-form-item label="客户" prop="region">
            <el-select style="width: 200px" v-model="ruleForm.region" placeholder="请选择客户">
              <el-option label="区域一" value="shanghai"></el-option>
              <el-option label="区域二" value="beijing"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="销售人员" prop="region">
            <el-select style="width: 200px" v-model="ruleForm.region" placeholder="请选择销售人员">
              <el-option label="区域一" value="shanghai"></el-option>
              <el-option label="区域二" value="beijing"></el-option>
            </el-select>
          </el-form-item>
          <el-button type="round" @click="openGoods" style="width: 150px;height: 30px;margin-left: 20px" icon="el-icon-shopping-cart-full">点击添加商品</el-button>
        </el-form>
      </div>

      <div class="commodity_form">
        <el-table
            class="el-table"
            :data="tableData"
            border
            show-summary
            style="width: 99%">
          <el-table-column
              prop="id"
              label=""
              width="100%"
          >

            <template slot-scope="scope">
              <i class="el-icon-circle-plus-outline" @click="openGoods"></i>

              <i class="el-icon-delete" @click="deleteGoods(scope.$index,tableData)"></i>
            </template>
          </el-table-column>
          <el-table-column
              prop="productName"
              label="产品名称"
              width="150%"
          >
          </el-table-column>
          <el-table-column
              prop="amount2"
              label="签单日期"
              width="150%"
          >
          </el-table-column>
          <el-table-column
              prop="amount3"
              label="付款金额"
              width="150%"
          >
          </el-table-column>
          <el-table-column
              prop="amount3"
              label="备注"
              width="150%"
          >
          </el-table-column>
          <el-table-column
              prop="amount3"
              label="数量"
              width="150%"
          >
          </el-table-column>
          <el-table-column
              prop="amount3"
              label="销售单价(元)"
              width="150%"
          >
          </el-table-column>
          <el-table-column
              prop="amount3"
              label="销售金额(元)"
              width="150%"
          >
          </el-table-column>
          <el-table-column
              prop="amount3"
              label="仓库"
              width="150%"
          >
          </el-table-column>
          <el-table-column
              prop="amount3"
              label="产品描述"
              width="150"
          >
          </el-table-column>
        </el-table>
      </div>

      <div class="goodsList">
        <el-dialog
            title="提示"
            :visible.sync="goodsDialogVisible"
            width="30%"
            :before-close="handleClose">
          <span>这是一段信息</span>
          <span slot="footer" class="dialog-footer">
          <el-button @click="goodsDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="goodsDialogVisible = false">确 定</el-button>
        </span>
        </el-dialog>
      </div>

      <div class="foot">
        <el-form :inline="true" size="mini" label-width="100px"  :model="ruleForm" :rules="rules" ref="ruleForm" class="demo-ruleForm">
          <el-form-item label="客户联系人" prop="region">
            <el-select style="width: 200px" v-model="ruleForm.region" placeholder="请选择客户">
              <el-option label="区域一" value="shanghai"></el-option>
              <el-option label="区域二" value="beijing"></el-option>
            </el-select>
          </el-form-item>

          <el-form-item label="联系人手机" prop="name">
            <el-input v-model="ruleForm.name" style="width: 200px"></el-input>
          </el-form-item>

          <el-form-item label="联系人电话" prop="name">
            <el-input v-model="ruleForm.name" style="width: 200px"></el-input>
          </el-form-item>

          <el-form-item label="客户地址" prop="name">
            <el-input v-model="ruleForm.name" style="width: 200px"></el-input>
          </el-form-item>
        </el-form>

      </div>

    </el-card>
  </div>
</template>

<script>
export default {
  name: "PurchaseOrder",
  data(){
    return{
      count: 0,
      goodsDialogVisible: false,
      value1: '',
      value2: '',
      ruleForm: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: ''
      },
      rules: {
        name: [
          { required: true, message: '请输入活动名称', trigger: 'blur' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ],
        region: [
          { required: true, message: '请选择活动区域', trigger: 'change' }
        ],
        date1: [
          { type: 'date', required: true, message: '请选择日期', trigger: 'change' }
        ],
        date2: [
          { type: 'date', required: true, message: '请选择时间', trigger: 'change' }
        ],
        type: [
          { type: 'array', required: true, message: '请至少选择一个活动性质', trigger: 'change' }
        ],
        resource: [
          { required: true, message: '请选择活动资源', trigger: 'change' }
        ],
        desc: [
          { required: true, message: '请填写活动形式', trigger: 'blur' }
        ]
      },
      tableData: [
        {
          id: '',
          name: '',
          amount1: '',
          amount2: '',
          amount3: ''
        },
        // {
        //   id: '12987123',
        //   name: '王小虎',
        //   amount1: '165',
        //   amount2: '4.43',
        //   amount3: 12
        // },
      ]
    }
  },
  methods:{
    openGoods(){
      this.$router.push({
        path: '/purchase/porderdetails'
      })
    },
    deleteGoods(index,tableData){
      console.log(index)
      this.tableData.splice(index,1);
      console.log(tableData)
    },
    handleClose(done) {
      this.$confirm('确认关闭？')
        .then(_ => {
          done();
        })
        .catch(_ => {});
    }
  }
}
</script>

<style scoped>
*{
  margin: 0;
  padding: 0;

}
.salesOrder{
  width: 100%;
}
.head{
  margin-top: 50px;
  width: 65%;
}
.commodity_form{
  margin-top: 50px;
}
.el-table{
  margin-left: 18px;
}
.el-icon-circle-plus-outline, .el-icon-delete{
  font-size: 20px;
  cursor: pointer;
}
.el-icon-delete,.el-icon-circle-plus-outline{
  margin-left: 12px;
}
.foot{
  margin-top: 50px;
  width: 65%;
}
.top{
  margin-top: 10px;
  position: absolute;
  width: 90%;
}
.top_left{
  font-size: 18px;
  float: left;
  margin-left: 30px;
}
.top_right{
  float: right;
}
</style>
