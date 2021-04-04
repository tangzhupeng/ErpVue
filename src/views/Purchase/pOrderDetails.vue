<template>
	<div>
	<el-row>
		<el-col :span="24">
			<div class="grid-content bg-purple-dark">
				<div class="title">
					销售出库单
				</div>
				<a class="back" >
					<i class="el-icon-arrow-left">返回</i>
					
				</a>
				<div class="pull-right">
					<el-button type="primary" size="small">驳回</el-button>
					<el-button type="primary" size="small">审批通过</el-button>
				</div>
			</div>		
			
		</el-col>
		
		
	</el-row>
	<div class="ikd-page-action-wrapper"></div>
	<div class="ikd-page-body">
		<div class="ikd-form-group">
			<label>编号：</label>
			<p class="ikd-form-control-static">XXXX00088</p>
		</div>
		<div class="ikd-form-group">
			<label>单据日期：</label>
			<p class="ikd-form-control-static">XXXX00088</p>
		</div>
		<div class="ikd-form-group">
			<label>交货日期：</label>
			<p class="ikd-form-control-static">XXXX00088</p>
		</div>
		<div class="ikd-form-group">
			<label>客户：</label>
			<p class="ikd-form-control-static">XXXX00088</p>
		</div>
		<div class="ikd-form-group">
			<label>销售人员：</label>
			<p class="ikd-form-control-static">XXXX00088</p>
		</div>
	</div>
	<div class="ikd-page-body">
		<div class="ikd-form-group">
			<label>客户联系人：</label>
			<p class="ikd-form-control-static">XXXX00088</p>
		</div>
		<div class="ikd-form-group">
			<label>联系人手机：</label>
			<p class="ikd-form-control-static">XXXX00088</p>
		</div>
		<div class="ikd-form-group">
			<label>联系人电话：</label>
			<p class="ikd-form-control-static">XXXX00088</p>
		</div>
	</div>
	<div class="ikd-page-body">
		<div class="ikd-form-group">
			<label>客户地址：</label>
			<p class="ikd-form-control-static">XXXX00088</p>
		</div>
		<div class="ikd-form-group">
			<label>创建时间:</label>
			<p class="ikd-form-control-static">XXXX00088</p>
		</div>
	</div>
	
	<el-table
    :data="tableData"
    border
	show-summary
    style="width: 100%">
    <el-table-column
      fixed
      prop="date"
      label="日期"
      width="150">
    </el-table-column>
    <el-table-column
      prop="name"
      label="姓名"
      width="120">
    </el-table-column>
    <el-table-column
      prop="province"
      label="省份"
      width="120">
    </el-table-column>
    <el-table-column
      prop="city"
      label="市区"
      width="120">
    </el-table-column>
    <el-table-column
      prop="address"
      label="地址"
      width="300">
    </el-table-column>
    <el-table-column
      prop="zip"
      label="邮编"
      width="120">
    </el-table-column>
	<el-table-column
 prop="zip"
  label="邮编"
  width="120">
	</el-table-column>
	<el-table-column
  prop="zip"
  label="邮编"
  width="120">
	</el-table-column>
	<el-table-column
  prop="zip"
  label="邮编"
  width="120">
	</el-table-column>
	<el-table-column
	prop="zip"
	label="邮编"
	width="120">
		</el-table-column>
   <!-- <el-table-column
      fixed="right"
      label="操作"
      width="100">
      <template slot-scope="scope">
        <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
        <el-button type="text" size="small">编辑</el-button>
      </template>
    </el-table-column> -->
  </el-table>
    <div class="ikd-page-action-wrapper"></div>
	</div>
</template>

<script>
 export default {
   methods: {
      handleClick(row) {
        console.log(row);
      }
    },
	
    data() {
      return {
        tableData: [
		{
          date: '2016-05-02',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 1
        }, {
          date: '2016-05-04',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1517 弄',
          zip: 1
        }, {
          date: '2016-05-01',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1519 弄',
          zip: 1
        }, {
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 1
        },
		{
			date: '2016-05-03',
			name: '王小虎',
			province: '上海',
			city: '普陀区',
			address: '上海市普陀区金沙江路 1516 弄',
			zip: 1
		},
		{
			date: '2016-05-03',
			name: '王小虎',
			province: '上海',
			city: '普陀区',
			address: '上海市普陀区金沙江路 1516 弄',
			zip: 1
		},
		]
      }
    }
  }
</script>

<style>
	.pull-right{
		float: right;
		margin-top: 5px;
	}
	.bg-purple-dark{
		width: 100%;
		height: 50px;
	}
	.title{
		display: block;
		float: left;
		height: 40px;
		font-size: 18px;
		line-height: 40px;
	}
	.back{
		cursor: pointer;
		float: left !important;
		color: #459df5;
		font-size: 14px;
		line-height: 32px !important;
		min-width: 70px;
		padding: 4px 10px;
		text-align: center;
   
	}
	.ikd-page-action-wrapper{
		height: 20px;
	}
	.ikd-page-body{
		padding-left: 15px;
		background-color: #FFFFFF;
		
	}
	.ikd-page-body>.ikd-form-group{
		display: inline-block;
		margin-right: 30px;
		font-size: 13px;
	}
	.ikd-page-body>.ikd-form-group>.ikd-form-control-static{
		display: inline-block;
		margin-left: 10px;
	}
	.ik-margin-vertical-10{
		margin-bottom: 10px;
		margin-top: 10px;
		border: 0;
		border-top: 1px solid #909399;
	}
</style>
