<template>
	<view>
		<!-- 基础用法 -->
		<list-section :title="'基础用法'" :iconStyle="'line'" :iconColor="'#26B1F6'" :titleColor="'#8CC7B5'"></list-section>
		<list-ul>
			<list-li :type="'base'" >
				<template v-slot:right>
					<view > 自定义 </view>
				</template>
			</list-li>
			<list-li :type="'base'" :content="'列表文字内容'"></list-li>
			<list-li :type="'base'" :title="'这是一个列表标题'" :note="'这是一个列表描述'"></list-li>
			<list-li :type="'base'" :disabled="true" :content="'禁用状态列表'"></list-li>
		</list-ul>
		
		<!-- 菜单列表 -->
		<list-section :title="'菜单列表'" :iconStyle="'line'" :iconColor="'#e03997'" :titleColor="'#ff0000'"></list-section>
		<list-ul>
			<list-li :type="'menu'" :iconImg="'https://img-cdn-qiniu.dcloud.net.cn/new-page/uni.png'" :content="'列表左侧带略缩图'" :rightText="'右侧文字'"></list-li>
			<list-li :type="'menu'" :iconType="'download'" :content="'列表右侧带箭头 + 角标'" :babgeNum="99" :isShowBadge="true" :rightText="'右侧的文字描述'"></list-li>
			<list-li :type="'menu'" :content="'列表右侧带 Switch'" :isShowSwitch="true" :originType="'11'" @switchChange="switchChange"></list-li>
			<list-li :type="'menu'" :content="'禁用状态'" :isShowSwitch="true" :disabled="true" :originType="'22'"></list-li>
			<list-li :type="'menu'" :content="'右边插槽自定义内容'" :isHover="false">
				<template v-slot:right>
					<view class="btn"> 按钮 </view>
				</template>
			</list-li>
		</list-ul>
		
		<!-- 消息列表 -->
		<list-section :title="'消息列表'" :iconStyle="'line'" :iconColor="'#8dc63f'" :titleColor="'#1890ff'"></list-section>
		<list-ul>
			<list-li 
			:type="'msg'" 
			:shape="'round'"
			:avatar="'https://ossweb-img.qq.com/images/lol/web201310/skin/big81020.jpg'"
			:title="'消息列表标题'"
			:note="'消息列表描述消息列表描述消息列表描述消息列表描述消息列表描述'"
			:time="'12:59'"
			:babgeNum="98"
			>
			</list-li>
		</list-ul>
		<list-li>
			<view style="height: 30px;text-align: center;background-color: #4CD964;color: #fff;line-height: 30px;"> 凑个数 </view>
		</list-li>
	</view>
</template>
<script>
	import listSection from '@/components/list/list-section.vue'
	import listUl from '@/components/list/list-ul.vue'
	import listLi from '@/components/list/list-li.vue'
	export default {
		components:{
			listUl,
			listSection,
			listLi
		},
		data() {
			return {
				
			}
		},
		methods: {
           switchChange(e,type){
			   console.log(e)
			   console.log(`开关事件来源类型：${type}`)
		   }
		}
	}
</script>
<style lang="scss" scoped>
	.btn{
		position: relative;
		border: 0upx;
		display: inline-flex;
		align-items: center;
		justify-content: center;
		box-sizing: border-box;
		padding: 0 30upx;
		font-size: 28upx;
		height: 64upx;
		line-height: 1;
		text-align: center;
		text-decoration: none;
		overflow: visible;
		margin-left: initial;
		transform: translate(0upx, 0upx);
		margin-right: initial;
		background-color: #f37b1d;
		color: #ffffff;
	}
</style>
