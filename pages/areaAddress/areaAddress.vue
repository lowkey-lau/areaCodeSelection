<template>
	<view>
		<areaAddress-directory :areaAddresss="areaAddresss" @paramClick="paramClick"></areaAddress-directory>
	</view>
</template>

<script>
	import areaAddressDirectory from '@/components/areaAddress-directory/areaAddress-directory.vue'
	export default {
		name:"areaAddresss",
		components:{
			areaAddressDirectory
		},
		data() {
			return {
				//示例数据
				areaAddresss:{
					"A": [{
						"id": 61,
						"spell": "australia",
						"name": '澳大利亚',
						"flagurl": "../../static/flag/icon-australia.png"
					}],
					"B": [{
						"id": 55,
						"spell": "brazil",
						"name": '巴西',
						"flagurl": "../../static/flag/icon-brazil.png"
					}],
					"C": [{
						"id": 86,
						"spell": "china",
						"name": '中国',
						"flagurl": "../../static/flag/icon-china.png"
					}],
					"G": [{
						"id": 49,
						"spell": "germany",
						"name": '德国',
						"flagurl": "../../static/flag/icon-germany.png"
					}],
					"H": [{
						"id": 852,
						"spell": "hongkong",
						"name": '中国香港',
						"flagurl": "../../static/flag/icon-hongkong.png"
					}],
					"I": [{
						"id": 91,
						"spell": "india",
						"name": '印度',
						"flagurl": "../../static/flag/icon-india.png"
					}],
					"I": [{
						"id": 81,
						"spell": "japan",
						"name": '日本',
						"flagurl": "../../static/flag/icon-japan.png"
					}],
					"K": [{
						"id": 82,
						"spell": "korea",
						"name": '韩国',
						"flagurl": "../../static/flag/icon-korea.png"
					}],
					"M": [{
						"id": 60,
						"spell": "malaysia",
						"name": '马来西亚',
						"flagurl": "../../static/flag/icon-malaysia.png"
					},{
						"id": 853,
						"spell": "macau",
						"name": '中国澳门',
						"flagurl": "../../static/flag/icon-macau.png"
					}],
					"R": [{
						"id": 7,
						"spell": "russia",
						"name": '俄罗斯',
						"flagurl": "../../static/flag/icon-russia.png"
					}],
					"S": [{
						"id": 65,
						"spell": "singapore",
						"name": '新加坡',
						"flagurl": "../../static/flag/icon-singapore.png"
					},{
						"id": 34,
						"spell": "spain",
						"name": '西班牙',
						"flagurl": "../../static/flag/icon-spain.png"
					}],
					"T": [{
						"id": 66,
						"spell": "thailand",
						"name": '泰国',
						"flagurl": "../../static/flag/icon-thailand.png"
					},{
						"id": 886,
						"spell": "taiwan",
						"name": '中国台湾',
						"flagurl": "../../static/flag/icon-taiwan.png"
					}],
					"U": [{
						"id": 1,
						"spell": "unitedstates",
						"name": '美国',
						"flagurl": "../../static/flag/icon-unitedstates.png"
					},{
						"id": 44,
						"spell": "unitedkingdom",
						"name": '英国',
						"flagurl": "../../static/flag/icon-unitedkingdom.png"
					}],
					"V": [{
						"id": 84,
						"spell": "vietnam",
						"name": '越南',
						"flagurl": "../../static/flag/icon-vietnam.png"
					}],
				}
			
			}
		},
		methods : {
			paramClick (e) {
				console.log(e)
				// uni.navigateTo({
				// 	url: '../register/register?zone=' + e.id + '&flagurl=' + e.flagurl 
				// })
			}
		}
	}
</script>

<style>

</style>
