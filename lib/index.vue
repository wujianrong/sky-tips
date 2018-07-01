<!--弹出框-->
<!--
	slot = content  
	内容区域快
	
	slot = btn 
	操作按钮块，不传的话，默认显示一个---”我知道了“----按钮
	
	
	showed  控制组件的显示隐藏   true   or   false
-->


<!--
	举例使用：
	在页面上直接
	<sky-tip :showed="ture">
  		<div slot="content" class="margin-top-md gray padding-sm">您已注册成功！初始登录密码是您手机号后六位，快去“个人信息”里修改登录密码吧！</div>
	</sky-tip>
  
-->



<template>
  <div class="tipsBox" v-show="show">
  	<div class="tip" ref="tipDom">
  		<i class="close iconfont icon-cuowu" @click="show=false"></i>
  		<div class="content">
  			<slot name="content"></slot>
  		</div>
  		<div class="tip-box">
  			<slot name="btn" v-if="btnShow"></slot>
  			<yd-button v-else class="sky-btn sky-btn-orange tip-btn" type="hollow"  @click.native="show=false">我知道了</yd-button>
  		</div>
  	</div>
  </div>
</template>

<script>
export default {
	name:'sky-tip',
	props:['showed'],
  data () {
    return {
      	show:true,
      	btnShow:false
    }
  },
  computed: {
      
  },
  methods: {
  	
  },
  mounted() {
  	this.$slots.btn ? this.btnShow = true : this.btnShow = false;
		this.$refs.tipDom.style.marginTop = -this.$refs.tipDom.clientHeight/2 +'px';
  },
  activated(){
 			if(this.showed) {
				this.show = true;
			}else {
				this.show = false;
			}
			this.$nextTick(()=>{
				this.$slots.btn ? this.btnShow = true : this.btnShow = false;
				this.$refs.tipDom.style.marginTop = -this.$refs.tipDom.clientHeight/2 +'px';
			})
  },
  watch: {
 			showed(val){
 				if(val) {
 					this.show = true;
 				}else {
 					this.show = false;
 				}
 			}
  }
}
</script>

<style scoped lang="less">
 .tipsBox {
 	position: fixed;
 	width: 100%;
 	height: 100%;
 	background: rgba(40,40,40,.6);
 	z-index: 9999;
	top: 0;
 	.tip {
 		padding: .3rem;
 		text-align: center;
 		width: 80%;
 		min-height: 4rem;
 		background: #FFFFFF;
 		position: fixed;
 		top: 50%;
 		left: 10%;
 		z-index: 9999;
 		padding-bottom: 1.4rem;
 		i.close {
		    position: absolute;
		    right: -.24rem;
		    top: -.24rem;
		    font-size: .48rem;
		    &:after {
		    	position: absolute;
			    content: '';
			    width: 50%;
			    height: 50%;
			    background: #FFFFFF;
			    top: 25%;
			    left: 25%;
			    z-index: -1;
		    }
 		} 
 		.tip-box {
 				text-align: center;
 				width: 80%;
	 			position: absolute;
	 			bottom: .4rem;
	 			left: 10%;
 			.tip-btn {
 				width: 100%;
 				height: .7rem;
	 			font-size: .28rem;
	 		}
 		}
 		
 	}
 }
 .content {
 	width: 100%;
 	white-space: normal;
  word-wrap: break-word;
  text-align: left;
 }
</style>
