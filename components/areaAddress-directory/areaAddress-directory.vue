<!-- programming by Lowkey-lau -->
<template>
	<view class="areaAddress-main">
		<!-- <view class="areaAddress-main-search">
			<navigator :url="'areaAddress-search?areaAddresss=' + areaAddresssEscape" hover-class="none">
				<input disabled="false" class="areaAddress-main-input" type="text" placeholder="请输入要搜索的联系人"/>
			</navigator>
		</view> -->
		<view class="areaAddressDirectory">
			<areaAddress-list 
			:areaAddresss="areaAddresss" 
			:letter="letter"
			:scrollAnimationOFF="scrollAnimationOFF" 
			@change="handlePhoneListIndex"
			@reset="handleReset"
			@handleClick="handleClick"
			>
			</areaAddress-list>
			<areaAddress-alphabet 
			:areaAddresss="areaAddresss"
			:areaAddressListIndex="areaAddressListIndex"
			@change="handleDatasetKey" 
			@scrollAnimationOFF="handleScrollAnimationOFF"
			@reset="handleReset"
			>
			</areaAddress-alphabet>
		</view>
	</view>
</template>

<script>
	import areaAddressList from './areaAddress-list.vue'
	import areaAddressAlphabet from './areaAddress-alphabet.vue'
	
	export default {
		name:"areaAddress-directory",
		components:{
			areaAddressList,
			areaAddressAlphabet
		},
		props:{
			areaAddresss:Object,
			default:false
		},
		data () {
			return {
				winHeight:0,
				letter : 'A',
				scrollAnimationOFF:true,
				areaAddressListIndex:'A',
				reset:true
			}
		},
		computed:{
			areaAddresssEscape () {
				return escape(JSON.stringify(this.areaAddresss))
			}
		},
		mounted () {
			let windowHeight = uni.getSystemInfoSync().windowHeight
			
			// #ifndef APP-PLUS
			this.winHeight = windowHeight
			//#endif
			
			//#ifdef APP-PLUS
			this.winHeight = windowHeight - 200
			//#endif
			
 			if(!this.areaAddresss){
				uni.showToast({
					title: '没有数据',
					icon:"none",
					mask: false,
					duration: 1500
				})
			}
		},
		methods:{
			handleClick (e) {
				this.$emit('paramClick',e)
			},
			handleDatasetKey (val) {
				this.letter = val
			},
			handleScrollAnimationOFF (val) {
				this.scrollAnimationOFF = val
			},
			handlePhoneListIndex(val){
				if(this.reset){
					this.areaAddressListIndex = val
				}
			},
			handleReset (val){
				if(val){
					this.letter = ''
				}
				this.reset = val
			}
			
		}
	}
</script>

<style>
.areaAddress-main{
	display: flex;
	flex-direction: column;
	overflow: hidden;
	height: 100vh;
	/* height: calc(100vh - 88upx); */
	/* #ifdef APP-PLUS */
	/* height: calc(100vh - var(--status-bar-height)); */
	/* #endif */
}
.areaAddressDirectory{
	display: flex;
	flex-direction: row;
	height: 100%;
	/* background-color: red; */
}
.areaAddress-main-search{
	background-color: #fff;
	padding: 10upx 20upx;
	border-bottom: 1px solid #e5e5e5;
}

.areaAddress-main-input{
	font-size:28upx;
	border: 1px solid #e5e5e5;
	border-radius: 3px;
	padding: 10upx 20upx 10upx 20upx;
}
</style>
