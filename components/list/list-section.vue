<template>
	<view 
	class="list-section" 
	:style="{height:listHeight,backgroundColor:listBgColor}">
		<view class="list-section-content">
			<view 
			v-if="!!iconStyle" 
			:class="[iconStyle==='line'?'list-section-line':iconStyle==='dot'?'list-section-dot':'']" 
			:style="{'backgroundColor':iconColor}"></view>
			<view :style="{color:titleColor,fontSize:fontSize}">{{title}}</view> 
		</view>
		<slot/>
		<view class="list-section-extra" v-if="isShowBtn">
			<view 
			class="list-btn" 
			hover-class="list-btn--hover" 
			:style="{color:btnTitleColor,fontSize:btnFontSize,borderRadius:borderRadius,backgroundColor:btnBgColor}"
			@click="btnHandler">{{btnTitle}}</view>
		</view>
	</view>
</template>
<script>
	export default {
		name:'list-section',
		props:{
			type:{
				type:String|Number,
				default:''
			},
			listHeight:{
				type:String,
				default:'50px'
			},
			listBgColor:{
				type:String,
				default:'#f8f8f8'
			},
			iconStyle:{
				type:String,
				default:''
			},
			iconColor:{
				type:String,
				default:'#c0c0c0'
			},
			title:{
				type:String,
				default:'默认标题'
			},
			titleColor:{
				type:String,
				default:'#333333'
			},
			fontSize:{
				type:String,
				default:'12px'
			},
			isShowBtn:{
				type:Boolean,
				default:false
			},
			btnTitle:{
				type:String,
				default:'按钮'
			},
			btnTitleColor:{
				type:String,
				default:'#ffffff'
			},
			btnFontSize:{
				type:String,
				default:'14px'
			},
			borderRadius:{
				type:String,
				default:'15px'
			},
			btnBgColor:{
				type:String,
				default:'#39b54a'
			}
		},
		data() {
			return {
				
			}
		},
		methods: {
			btnHandler(){
				this.$emit('onBtnClick',this.type)
			}
		}
	}
</script>
<style lang="scss" scoped>
	.list-section{
		margin-top:20upx;
		padding: 0 10px;
		min-height: 88upx;
		height: 100upx;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		position: relative;
		.list-section-content{
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
			.list-section-line{
				height: 15px;
				background-color: #c0c0c0;
				border-radius: 5px;
				width: 3px;
				margin-right:28upx;
			}
			.list-section-dot{
				height: 8px;
				background-color: #f37b1d;
				border-radius: 50%;
				width: 8px;
				margin-right: 20upx;
			}
		}
		.list-section-extra{
			.list-btn{
				box-shadow: 3px 3px 4px rgba(48, 156, 63, 0.2);
				box-sizing: border-box;
				padding: 0 30upx;
				height: 60upx;
				display: flex;
				flex-direction: row;
				text-align: center;
				align-items: center;
				
			}
			.list-btn--hover{
				opacity: .8;
			}
		}
	}
</style>
