<template>
	<view class="list-group" :style="{backgroundColor:bg}">
		<slot/>
	</view>	
</template>
<script>
	export default {
		name:'list-group',
		props:{
			bg:{
				type:String,
				default:'#ffffff'
			}
		},
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>
<style lang="scss" scoped></style>
