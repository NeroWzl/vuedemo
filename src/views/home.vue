<template>
	<div class="home">
		<div>
			<el-row>
				<el-col :span='7' id='list1'>
					<el-tabs @tab-click="handleClick">
						<el-tab-pane label="点餐">
							<el-table :data="tableData1" border show-summary style="width: 100%">
								<el-table-column prop="name" label="商品" ></el-table-column>
								<el-table-column prop="count" label="数量"></el-table-column>
								<el-table-column prop="price" label="金额"></el-table-column>
								<el-table-column label='操作'>
									<template slot-scope='scope'>
										<el-button type='text' size='small' @click="del(scope.$index)">删除</el-button>
	                                    <el-button type='text' size='small' @click="add(scope.$index)">增加</el-button>
									</template>
								</el-table-column>
							</el-table>	
							<div class="order-btn">
								<el-button type="danger" @click="clear()">删除</el-button>
								<el-button type="success" @click="submit()">结账</el-button>
							</div>
						</el-tab-pane>
						<el-tab-pane label="外卖" >
							<el-table :data="tableData2" border show-summary style="width: 100%">
								<el-table-column prop="name" label="商品" ></el-table-column>
								<el-table-column prop="count" label="数量"></el-table-column>
								<el-table-column prop="price" label="金额"></el-table-column>
								<el-table-column label='操作'>
									<template slot-scope='scope'>
										<el-button type='text' size='small' @click="del(scope.$index)">删除</el-button>
	                                    <el-button type='text' size='small' @click="add(scope.$index)">增加</el-button>
									</template>
								</el-table-column>
							</el-table>	
							<div class="order-btn">
								<el-button type="danger" @click="clear()">删除</el-button>
								<el-button type="success" @click="submit()">结账</el-button>
							</div>
						</el-tab-pane>
					</el-tabs>
				</el-col>
				<el-col :span='15' id='list2'>
					<div class="product">
						<div class="title">常用商品</div>
						<div class="pro-list">
                            <ul>
                               <li v-for='item in hotPros'>
                                   <span>{{item.name}}</span>
                                   <span class="pro-pri">￥{{item.pri}}</span>
                               </li>
                            </ul>
                        </div>
					</div>
					<div class="pro-type">
                        <el-tabs>
                            <el-tab-pane label='肥宅区'>
                                <ul class="ckList">
                                    <li v-for='val in goodType1'>
                                        <span class="foodImg"><img :src="val.img" ></span>
                                        <span class="foodName">{{val.name}}</span>
                                        <span class="foodPri">￥{{val.pri}}</span>
                                    </li>
                                    <h1 style="clear: both;"></h1>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label='儿童区'>
                                <ul class="ckList">
                                    <li v-for='val in goodType2'>
                                        <span class="foodImg"><img :src="val.img" alt=""></span>
                                        <span class="foodName">{{val.name}}</span>
                                        <span class="foodPri">￥{{val.pri}}</span>
                                    </li>
                                    <h1 style="clear: both;"></h1>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label='LLY区'>
                                <ul class="ckList">
                                    <li v-for='val in goodType3'>
                                        <span class="foodImg"><img :src="val.img" alt=""></span>
                                        <span class="foodName">{{val.name}}</span>
                                        <span class="foodPri">￥{{val.pri}}</span>
                                    </li>
                                    <h1 style="clear: both;"></h1>
                                </ul>
                            </el-tab-pane>
                        </el-tabs>
                   </div>
				</el-col>
			</el-row>
		</div>
	</div>
</template>

<script>
	import axios from 'axios'
	export default {
		name: 'home',
		data() {
			return {
				tableData1:[],
				tableData2:[],
				hotPros:[],
				goodType1:[],
				goodType2:[],
				goodType3:[],
				sel:0,
				num:0
			}
		},
		mounted(){
			let h = document.body.clientHeight;
			let list1 = document.querySelector('#list1')
			let list2 = document.querySelector('#list2')
			list1.style.height=h+'px'
			list2.style.height=h+'px'
		},
		created(){
			axios.get('../../static/data.json')
	        .then(res => {
	            this.tableData1 = res.data.tableData1;
	            this.tableData2 = res.data.tableData2;
	            this.hotPros = res.data.hotPros;
	            this.goodType1 = res.data.goodType1;
	            this.goodType2 = res.data.goodType2;
	            this.goodType3 = res.data.goodType3;
	        })
	        .catch(err => {
	            console.log('网络出错，无法访问')
	        })
		},
		methods:{
			add(i){
				if(this.sel==0){
					this.tableData1[i].count++
				}else if(this.sel==1){
					this.tableData2[i].count++
				}
			},
			del(i){
				if(this.sel==0){
					this.tableData1.splice(i,1)
				}else if(this.sel==1){
					this.tableData2.splice(i,1)
				}
			},
			clear(){
				let check = confirm('确定清空点餐？')
				if(check){
					if(this.sel==0){
						this.tableData1=[]
					}else if(this.sel==1){
						this.tableData2=[]
					}
				}else{
					return false
				}
			},
			submit(){
				const that = this;
				if(this.sel==0){
					let asd=0
					this.tableData1.map(function(v){
						that.num += (v.count*v.price)
					})
				}else if(this.sel==1){
					
				}
			},
			handleClick(event) {
	        	if(event.index==0){
	        		this.sel=0
	        	}else if(event.index==1){
	        		this.sel=1
	        	}
	      	}
		}
	}
</script>

<style>
.title{
	height: 40px;
	background-color: #3190E8;
	font-size: 24px;
	color: white;
	line-height: 40px;
}
.pro-list{
	padding-top: 10px;
}
.pro-list ul{
	display: flex;
	justify-content: space-around;
	flex-wrap: wrap;
}
.pro-list ul li{
	list-style: none;
	width: 20%;
	height: 50px;
	border: 1px solid #FFCD58;
	line-height: 50px;
	text-align: center;
	margin: 10px 0;
	cursor: pointer;
}
.pro-list span{
	font-size: 20px;
	font-weight: bold;
	color: #777777;
}
.pro-list .pro-pri{
	font: 18px normal;
	color: #EE0F42;
}
.ckList{
	padding: 0 10px;
}
.ckList li{
	list-style: none;
	float: left;
	width: 20%;
	border: 1px solid #FFCD58;
	cursor: pointer;
	margin: 10px;
}
.foodImg img{
	width: 100%;
	
} 
.foodName{
	font-size: 24px;
	color: #777777;
}
.foodPri{
	font-size: 20px;
	color: #EE0F42;
}
</style>