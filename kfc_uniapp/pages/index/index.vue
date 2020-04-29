<template>
	<view class="big">
		<van-sidebar :active-key="activeKey">
			<van-sidebar-item :title="item.name" @click="lick" v-for="(item,index) in list" :key="index" />
		</van-sidebar>
		<view class="com" @click="li">
			<view class="commdity" v-for="(com,index) in commdity" :key="com.id">
				<image :src="com.photo"></image>
				<text class="name">{{com.name}}</text>
				<text class="price">￥{{com.price}}.0<text style="font-size: 12px;">起</text></text>
				<van-stepper :value="com.num" @change="onChange" :data-index="index" class="step" min="0" max="10" />
			</view>
		</view>
		<view class="but" v-show="but" @click="butt">
			<view class="shop">
				<image src="../../static/肯德基.png" class="logo"></image>
				<van-tag round type="warning">{{totalnum}}</van-tag>
				<text class="total">￥{{total}}.0</text>
				<view class="rig">
					<text class="xuanhaole">选好了</text>
					<text class="order">order</text>
				</view>
			</view>
		</view>
		<view class="pull" v-show="show">
			<view class="shopdetails" v-for="(shopcom,index) in commdity" :key="shopcom.id" v-if="shopcom.num">
				<text style="position: absolute;margin: 0 0 0 5%;">{{shopcom.name}}</text>
				<text style="color: #D62F35;position: absolute;margin: 0 0 0 50%;">￥{{shopcom.price}}.0</text>
				<van-stepper :value="shopcom.num" @change="onChange" :data-index="index" min="0" max="10" class="tstep" />
			</view>
			<!-- <van-popup :show="show" closeable position="bottom" custom-style="height: 20%" @close="onClose" /> -->
		</view>
	</view>
</template>

<script>
	import Notify from 'wxcomponents/vant/notify/notify';
	export default {
		data() {
			return {
				activeKey: 0,
				but: false,
				show: false,
				total:'',
				totalnum:'',
				list: [{
						id: 1,
						name: '人气热卖'
					},
					{
						id: 2,
						name: '潮汉堡'
					},
					{
						id: 3,
						name: '桶'
					}
				],
				commdity: [{
						id: 1,
						name: '花花五一世界桶',
						price: '95',
						photo: '../../static/五一世界桶.png',
						num: 0
					},
					{
						id: 2,
						name: '五一小食桶',
						price: '59',
						photo: '../../static/五一小食桶.png',
						num: 0
					},
					{
						id: 3,
						name: '宝可梦牛五方双人餐',
						price: '62',
						photo: '../../static/宝可梦双人餐.png',
						num: 0
					},
					{
						id: 4,
						name: '五一大食桶',
						price: '59',
						photo: '../../static/五一大食桶.png',
						num: 0
					},
					{
						id: 5,
						name: '川辣椒牛五方',
						price: '59',
						photo: '../../static/川辣椒.png',
						num: 0
					}
				]
			}
		},
		onLoad() {

		},
		methods: {
			li(){
				this.show = false;
			},
			//步进器
			onChange(event) {
				// console.log(event.detail);
				// console.log(event.currentTarget.dataset.index)
				this.commdity[event.currentTarget.dataset.index].num = event.detail;
				// console.log(this.commdity)
				if (this.totalnum >= 0) {
					this.but = true;
				}
				this.step()
				if(this.totalnum == 0){
					this.show = false;
					this.but = false;
				}
			},
			//侧边导航
			lick(event) {
				var that = this
				// console.log(event.detail)
				console.log(that.commdity)
			},
			step() {
				var totalnum = 0;
				var total = 0;
				for (let c in this.commdity) {
					totalnum += this.commdity[c].num
					total += this.commdity[c].price * this.commdity[c].num
				}
				console.log('总数量：'+totalnum)
				// console.log(total)
				this.total = total;
				this.totalnum = totalnum;
			},
			onClose() {
			    this.show= false;
			},
			butt(){
				this.show = !this.show ;
				// if(this.show){
				// 	this.show = true;
				// }else{
				// 	this.show = false;
				// }
			}
		}
	}
</script>

<style>
	.big {
		height: 1500rpx;
	}

	.com {
		width: 80%;
		height: 120px;
		margin: -40% 0 0 20%;
	}

	.commdity {
		border: solid 1px #F6F6F6;
	}

	.commdity image {
		width: 45%;
		height: 120px;
	}

	.name {
		position: absolute;
		margin: 2% 0 0 12%;
		font-size: 32rpx;
	}

	.price {
		font-weight: bold;
		font-size: 20px;
		color: #E02D3F;
		position: absolute;
		margin: 12% 0 0 20%;
	}

	.step {
		position: absolute;
		margin: 22% 0 0 15%;
	}

	.but {
		width: 100%;
		height: 60px;
		bottom: 0;
		position: fixed;
		background-color: #D62F35;
		color: #FFFFFF;
		z-index: 2;
	}

	.shop {
		display: flex;
	}

	.logo {
		width: 15%;
		height: 50px;
	}

	.total {
		font-size: 56rpx;
		color: #FFFFFF;
		margin: 2%;
	}

	.rig {
		width: 30%;
		border-left: solid 1px #FFFFFF;
		margin: 0 0 0 20%;
	}

	.xuanhaole {
		font-size: 40rpx;
		color: #FFFFFF;
		position: relative;
		top: 5%;
		left: 40%;
	}

	.order {
		font-size: 30rpx;
		position: relative;
		top: 40%;
		right: 5%;
	}

	.pull {
		width: 100%;
		height: 150px;
		background-color: #FFFFFF;
		bottom: 9%;
		position: fixed;
		z-index: 3;
	}
	.shopdetails{
		height: 30px;
		display: flex;
		/* justify-content: space-around; */
		font-size: 38rpx;
	}
	.tstep{
		position: absolute;
		right: 0;
	}
</style>
