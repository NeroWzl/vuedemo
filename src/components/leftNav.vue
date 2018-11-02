<template>
  <div class="left-nav">
  	<ul>
  		<li :class="">
  			<i class="iconfont icon-shouye"></i>
  			<p>首页</p>
  		</li>
  		<li>
  			<i class="iconfont icon-gouwuche"></i>
  			<p>购物</p>
  		</li>
  		<li>
  			<i class="iconfont icon-liwu"></i>
  			<p>福利</p>
  		</li>
  		<li>
  			<i class="iconfont icon-shouhuodizhi"></i>
  			<p>收货</p>
  		</li>
  	</ul>
  </div>
</template>

<script>
export default {
  name: 'leftNav',
  data () {
    return {
      
    }
  }
}
</script>

<style scoped>
	.left-nav{
		width: 5%;
		height: 100%;
		float: left;
		background-color: #00a6ff;
	}
	.iconfont{
		font-size: 24px;
	}
	.left-nav li{
		list-style: none;
		width: 100%;
		text-align: center;
		border-bottom: 1px solid #2C3E50;
		padding: 10px 0;
	}
	.left-nav li:hover{
		
	}
</style>
