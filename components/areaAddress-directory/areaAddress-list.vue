<!-- programming by Lowkey-lau -->
<template>
	<view class="scroll-main">
		<scroll-view class="scroll-list"
		:scroll-top="1"
		scroll-y="true"
		:scroll-with-animation="scrollAnimationOFF" 
		:scroll-into-view="scrollViewId" 
		@scroll="handleScroll">
			<view class="areaAddress-list">
				<view class="list-item" 
				v-for="(item, key) of areaAddresss" 
				:key="key" 
				:id="key">
					<view class="list-item-title">{{key}}</view>
					<view class="list-item-areaAddress" 
					@click="handleClick"
					hover-class="commonly-hover" 
					:hover-start-time="20" 
					:hover-stay-time="70" 
					v-for="innerItem in item"
					:key="innerItem.id"
					:data-name="innerItem.name"
					:data-id="innerItem.id"
					:data-flagurl="innerItem.flagurl"
					:data-areaAddressnumber="innerItem.areaAddressnumber"
					>
						<view class="flag">
							<image :src="innerItem.flagurl" mode="widthFix"></image>
						</view>
						<view class="name">
							{{innerItem.name}}
						</view>
						<view class="code">
							+{{innerItem.id}}
						</view>
					</view>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		name:"areaAddress-list",
		props:{
			areaAddresss:Object,
			letter:String,
			scrollAnimationOFF:Boolean
		},
		data () {
			return {
				winHeight:0,
				scrollTop:0,
				letterDetails:[],
				timer:null
			}
		},
		computed:{
			scrollViewId () {
				return this.letter
			}
		},
		mounted(){
			// // #ifndef APP-PLUS
			// this.winHeight = uni.getSystemInfoSync().windowHeight
			// //#endif
			// 
			// //#ifdef APP-PLUS
			// this.winHeight = uni.getSystemInfoSync().windowHeight
			// //#endif

		},
		methods:{
			handleClick (e) {
				console.log(e);
				this.$emit('handleClick',e.currentTarget.dataset)
			},
			handleScroll (e){
				if(this.letterDetails.length === 0){
					let view = uni.createSelectorQuery().selectAll('.list-item')
					view.boundingClientRect(data=>{
						let top = data[0].top
						data.forEach((item,index)=>{
							item.top = item.top - top
							item.bottom  = item.bottom - top
							this.letterDetails.push({
								id:item.id,
								top:item.top,
								bottom:item.bottom
							})
						})
					}).exec()	
				}
				
				const scrollTop = e.detail.scrollTop
				this.letterDetails.some((item,index)=>{
					if(scrollTop>=item.top && scrollTop <= item.bottom - 5){
						this.$emit('change',item.id)
						this.$emit('reset',true)
						return true
					}
				})
			}
		}
			
	}
</script>

<style scoped lang="scss">
	.scroll-main{
		flex: 1;
	}
	.commonly-hover{
		background-color: #eee;
	}
	
	.scroll-list{
		flex: 1;
		height: 100vh;
		overflow-y: hidden;
	}

	.areaAddress-list{
		display: flex;
		background-color: #fff;
		overflow: hidden;
		flex-direction:column;
		position:relative;
		width: 100%;
		height: auto;
		flex: 1;
	}
	
	.list-item {
		width: 100%;
		display: flex;
		align-items: center;
		flex-wrap:wrap;
		height: 60upx;
		background-color: #fff;
		height: 100%;
		
	}
	
	.list-item >.list-item-areaAddress{
		font-weight: normal;
	}
	
	.list-item-title{
		background-color: #eee;
		padding: 10upx 20upx;
		font-weight: bold;
		width: 100%;
	}
	
	.list-item-areaAddress{
		width: 100%;
		// height: 60upx;
		// line-height: 60upx;
		font-size: 26upx;
		font-weight: bold;
		padding: 30upx 20upx;
		color: #333;
		border-bottom: 1px solid #e5e5e5;
		display: flex;
		align-items: center;
		.flag{
			width: 60upx;
			margin-right: 30upx;
			image{
				width: 100%;
				display: block;
			}
		}
		.name{
			margin-right: 30upx;
		}
	}
</style>
