<template>
	<view class="list-li-container">
		<!-- 基础用法 -->
		<view class="list-li"  v-if="type=='base'" :class="[disabled?'disabled':'']">
			<view class="list-li-cell">
				<view class="list-cell-content">
					<template v-if="content.length">
						{{content}}
					</template>
					<template  v-else-if="note.length || title.length">
						<view class="list-cell-content-title">{{title}}</view>
						<view class="list-cell-content-note">{{note}}</view>
					</template>
					<template v-else>
						<slot name="right"></slot>
					</template>
				</view>
			</view>
		</view>
		
		<!-- 菜单列表 -->
		<view class="list-li" :hover-class="hoverClass" v-else-if="type=='menu'" :class="[disabled?'disabled':'']">
			<view class="list-li-cell">
				<view class="list-cell-icon" v-if="!!iconImg || !!iconType">
					<icon v-if="!!iconType" :type="iconType" size="26"/>
					<image v-if="!!iconImg" class="img" :src="iconImg">
				</view>
				<view class="list-cell-content">{{content}}</view>
				<view class="list-right" :class="[(isShowSwitch || !isHover)?'':'arrow-right']">
					<template v-if="isShowSwitch">
						<switch :disabled="disabled"  @change="switchChange" />
					</template>
					<template v-else-if="isShowBadge">
						<view class="list-cell-badge" :style="{backgroundColor:badgeBgColor,color:badgeColor}" v-if="babgeNum!=0">{{babgeNum}}</view>
					</template>
					<template v-else-if="rightText.length">
						{{rightText}}
					</template>
					<template>
						<slot name="right"></slot>
					</template>
				</view>
			</view>
		</view>
		<view class="list-li" v-else-if="type=='msg'" hover-class="list-li--hover" :class="[disabled?'disabled':'']">
			<view class="list-li-cell">
				<view class="list-cell-avatar" v-if="avatar.length"><image :src="avatar" :style="{borderRadius:shape=='round'?'1000px':'10px'}"></image></view>
				<view class="list-cell-content" style="max-width:500upx">
					<view class="list-cell-msg-title">{{title}}</view>
					<view class="list-cell-msg-note">{{note}}</view>
				</view>
				<view class="list-msg-right">
					<view class="list-msg-top" v-if="time.length">{{time}}</view>
					<view class="list-msg-bottom"><view class="list-msg-badge" v-if="babgeNum!=0">{{babgeNum}}</view></view>
				</view>
			</view>
		</view>
		<view v-else>
			<slot/>
		</view>
	</view>	
</template>
<script>
	export default {
		name:'list-li',
		props:{
			type:{
				type:String | Number,
				default:''
			},
			disabled:{
				type:Boolean,
				default: false
			},
			content:{
				type:String,
				default: ''
			},
			title:{
				type:String,
				default: ''
			},
			note:{
				type:String,
				default: ''
			},
			rightText:{
				type:String,
				default: ''
			},
			iconImg:{
				type:String,
				default:''
			},
			iconType:{
				type:String,
				default:''
			},
			isShowBadge:{
				type:Boolean,
				default:false
			},
			isShowSwitch:{
				type:Boolean,
				default:false
			},
			babgeNum:{
				type:String | Number,
				default:''
			},
			isHover:{
				type:Boolean,
				default:true
			},
			badgeBgColor:{
				type:String,
				default: '#4cd964'
			},
			badgeColor:{
				type:String,
				default: '#ffffff'
			},
			avatar:{
				type:String,
				default:''
			},
			shape:{
				type:String,
				default:''
			},
			time:{
				type:String,
				default:''
			},
			originType:{
				type:String | Number,
				default:''
			}
		},
		computed:{
			hoverClass(){
				return (this.isShowSwitch || !this.isHover)?'':'list-li--hover'
			}
		},
		data() {
			return {
				
			}
		},
		methods: {
			switchChange(e){
				this.$emit('switchChange',e.detail.value, this.originType)
			}
		}
	}
</script>
<style lang="scss" scoped>
	.list-li-container{
		.disabled{
			opacity: 0.3;
		}
		.list-li{
			padding-left: 30upx;
			.list-li-cell{
				display: flex;
				flex-direction: row;
				justify-content: space-between;
				position: relative;
				padding: 24upx 30upx 24upx 0;
				.list-cell-avatar{
					width: 96upx;
					height: 96upx;
					margin-right: 20upx;
					image{
						width: 100%;
						height: 100%;
					}
				}
				.list-cell-icon{
					width: 52upx;
					height: 52upx;
					margin-right: 18upx;
					.img{
						width: 100%;
						height: 100%;
					}
				}
				.list-cell-content{
					flex: 1;
					font-size: 14px;
					color: #3b4144;
					line-height: 1.8;
					.list-cell-msg-title{
						
					}
					.list-cell-msg-note{
						max-width: 500upx;
						margin-top: 3px;
						color: #999;
						font-size: 12px;
						overflow: hidden;
						word-break: break-all;  /* break-all(允许在单词内换行。) */
						text-overflow: ellipsis;  /* 超出部分省略号 */
						display: -webkit-box; /** 对象作为伸缩盒子模型显示 **/
						-webkit-box-orient: vertical; /** 设置或检索伸缩盒对象的子元素的排列方式 **/
						-webkit-line-clamp: 1; /** 显示的行数 **/
					}
					.list-cell-content-title{
						
					}
					.list-cell-content-note{
						margin-top: 3px;
						color: #999;
						font-size: 12px;
						overflow: hidden;
					}
				}
				.list-msg-right{
					flex-direction: column;
					text-align: center;
					display: flex;
					align-items: center;
					justify-content: space-around;
					.list-msg-top{
						color: #8799a3;
						font-size: 10px;
					}
					.list-msg-bottom{
						.list-msg-badge{
							font-size: 12px;
							color: #fff;
							background-color: #e54d42;
							padding: 0 12upx;
							border-radius: 100upx;
							display: flex;
							align-items: center;
							justify-content: center;
						}
					}
					
				}
			}
			.list-right{
				color: #999;
				font-size: 12px;
				display: flex;
				flex-direction: row;
				align-items: center;
				.list-cell-badge{
					font-size: 12px;
					padding: 0 12upx;
					border-radius: 100upx;
					display: flex;
					align-items: center;
					justify-content: center;
				}
			}
			.arrow-right{
				padding-right: 38upx;
			}
			.arrow-right::after{
				content: " ";
				display: block;
				border: solid #888888;
				border-width: 0 1px 1px 0;
				display: inline-block;
				padding: 3px;
				transform: rotate(-45deg) translateY(-50%);
				position: absolute;
				right: 10rpx;
				top: 50%;
			
			}
			.list-li-cell::after{
				position: absolute;
				bottom: -1px;
				right: 0;
				left: 0;
				height: 1px;
				content: '';
				transform: scaleY(.5);
				background-color: #e5e5e5;
			}
		}
		.list-li--hover{
			background-color: #f1f1f1;
		}
		
	}
</style>
