<!--	复核总部	-->
<template>
	<div v-if="visible">
		<div class="modal fade in" id="myModal" style="display: block; padding-right: 21px;">
	        <div class="modal-dialog">
	            <div class="modal-content">
	                <div class="modal-header">
	                    <button type="button" class="close" data-dismiss="modal" aria-hidden="true" @click="close">×</button>
	                    <h4 class="modal-title" id="myModalLabel">项目管理 > 已激活 > 查看 > 批量设置 > 复核总部</h4>
	                </div>
	                <div class="modal-body">
	                	<div class="button-div">
		                    <el-button type="primary" class="btn btn-default fuheBut"><span class="fa fa-save" style="padding-right:10px;"></span>确认</el-button>
		                    <el-button @click="close" type="primary" class="btn btn-default fuheBut"><span class="fa fa-upload" style="padding-right:10px;"></span>取消</el-button>
	                  	</div>
	                  	<hr>
	                  	<div style="height:100%">
		                	<table id="customerTable" cellspacing="0" width="100%" class="table table-striped" >
		                        <thead class="unitThead">
		                          <tr>
		                              <th width="30"><span class="glyphicon glyphicon-search" id="dataSearch"></span></th>
		                              <th>名称</th>
		                              <th>编码</th>
		                              <th>简称</th>
		                              <th>上级</th>
		                              <th>描述</th>
		                              <th>类型</th>
		                          </tr>
		                        </thead>
		                        <tbody class="cutTaBody">
		                          <template v-for="(item,key) in list">
		                            <tr>
		                              <td>{{key+1}}</td>
		                              <td>{{item.Name}}</td>
		                              <td>{{item.Code}}</td>
		                              <td>{{item.ShortName}}</td>
		                              <td>{{item.ParentId.Name}}</td>
		                              <td>{{item.Description}}</td>
		                              <td>{{item.Type.text}}</td>
		                            </tr>
		                          </template>

		                        </tbody>
		                    </table>
	                    </div>
	                  	<div style="clear:both"></div>
	                </div>

	            </div>
	            <!-- /.modal-content -->
	        </div>
	        <!-- /.modal-dialog -->
	    </div>
	</div>
</template>

<script>
import axios from 'axios'
import qs from 'qs'
export default{
	data() {
		return{
			list: [],
		}
	},
	props: {
		visible: Boolean
	},
	methods: {
		close () {
	      this.$emit('close');
	    },
	},
	beforeMount() {
		var self = this
	    var getCodePars = {
	    	'limit': "5",
	    	'page': "1",
	    	'p_schema': "Orgs/DeptSelectFrom",
	    	'start': "0",
	    	'filter': "[]",
	    	'isSelect': "false",
	    	'sort': "[]"
	    }
	    axios.post("http://dingxin.cmsmate.cn:80/form/list",
	        qs.stringify(getCodePars)
	        , {
	        headers: {'Content-Type': 'application/x-www-form-urlencoded'},
	      })
	    .then(function (response) {
	    	self.list = JSON.parse(response.data.data)
	    	self.list = self.list.Data
	    	console.log(self.list)
	    })
	    .catch(function (error) {
	      console.log(error);
	    });
	}
}
</script>

<style scoped lang="scss">
/**	对话框样式	**/
#addModal {margin-top: 200px; }
.modal-dialog {width: 1300px;}
.modal-content{}
.modal-header{background-color: #1dbba4; color:#fff;font-family:"Microsoft YaHei",Arial,Helvetica,sans-serif,"微软雅黑";}
.modal-header button{color: red;font-size: 24px;}
.modal-title{font-weight: normal; }
.cusGroup{height: 36px;line-height: 36px;}
.cusConLabel{text-align: right;}
.button-div{margin-left: 20px;margin-top: 10px;}
.modal{z-index: 1080;}
.modal-backdrop{z-index: 1060;}

#cusTool{float:left;}
.toolSearch{margin-bottom: 0px;}
.cusAdd{background-color: #fff!important;color: #1dbba4 !important;border: 1px solid #1dbba4 !important;}
.cusAdd:hover{background-color: #1dbba4!important;color: #ffffff !important;}
.cusPus{padding-right: 6px !important;}
.clear{clear: both;}
.cusSearch input{display: block;width: 100%;height: 30px;padding: 6px 12px;font-size: 14px;line-height: 1.42857143;color: #555;background-color: #fff;background-image: none;border: 1px solid #ccc;border-radius: 4px;-webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075);box-shadow: inset 0 1px 1px rgba(0,0,0,.075);-webkit-transition: border-color ease-in-out .15s,-webkit-box-shadow ease-in-out .15s;-o-transition: border-color ease-in-out .15s,box-shadow ease-in-out .15s;transition: border-color ease-in-out .15s,box-shadow ease-in-out .15s;}
.cusFoot{ height: 40px;}
.cusPagNum{ text-align: right;height: 40px; line-height: 40px;
  .pagination{margin: 0px;}
}
.cusTabInfo{height: 40px;line-height: 40px;}
.table{margin-bottom: 10px; border-bottom: 1px solid #cdcece;}

.button-div{margin-left: 20px;margin-top: 10px;margin-bottom: 10px;}
.fuheBut{background-color:#ffffff;color: #1dbba4;border: 1px #1dbba4 solid;}
.fuheBut:hover{background-color:#1dbba4;color: #ffffff;border: 1px #1dbba4 solid;}
.table>thead>tr>th{font-weight: 400}
thead {background-color: #1dbba4}
tbody tr:hover{
  background-color: #C9E9E5;
}
</style>