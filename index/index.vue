<template>
	<view>

		<!-- 转盘 -->
		<view @click="cjShow = true" class="left_top">
			
		</view>
		<!-- 转盘 -->

		<!-- 转盘弹出 -->
		<view v-if="cjShow == true" style="width: 100vw;height: 100vh;background-color: rgba(0,0,0,0.4);position: fixed;top: 0;left: 0;z-index: 99999;display: flex;flex-flow: column;justify-content: center;align-items: center;">
			<text @click="cjShow = false" class="iconfont" style="color: #FFFFFF;font-size: 16px;position: absolute;top: 60px;right: 20px;">关</text>
			
			<!-- 谷歌浏览器下面的实例包含了-webkit-前缀。 -->
			<view style="position: relative;display: flex;flex-flow: column;justify-content: center;align-items: center;">
				<!-- 转盘旋转盒子 -->
				<view class="turn" :class="'cjstar' + cjName">
					<!-- 转盘背景 -->
						<image src="../../static/zpbg.png" style="width: 300px;height: 300px;position: absolute;top: 0px;"></image>
					<!-- 转盘背景 -->
					<!-- item -->
					<view v-for="(resCJData_item, resCJData_index) in resCJData" :key="resCJData_index" :class="'cj-item'+resCJData_index" class="cjItemStyle">
						<!-- 内容标题 -->
							{{resCJData_item.name}}
						<!-- 内容标题 -->
						<!-- 内容图片 -->
							<image :src="resCJData_item.image" style="width: 36px;height: 40px;"></image>
						<!-- 内容图片 -->
					</view>
					<!-- item -->
				</view>
				<!-- 转盘旋转盒子 -->
				<!-- 点击按钮 -->
					<image @click="cjReq()" src="../../static/star.png" style="width: 64px;height: 72px;position: absolute;top: 108px;"></image>
				<!-- 点击按钮 -->
			</view>
			

		</view>
		<!-- 转盘弹出 -->


	</view>
</template>

<script>
	/*			2020-7-29 基于项目功能完成，并提取予后期复用
		
		抽奖转盘效果 
		效果图：https://gaojuqian.com/github/img/cj.gif
		使用将index做路由放入文件夹，以及static图片
		可以用于uni-app项目 h5,小程序等,app未测试
		*如果用于vue cli请自行调整, <view> 改为 <div>
	*/
	export default {

		data() {
			return {
				cjShow: false, // 抽奖弹窗show
				cjName: 0, // 转盘旋转位置
				resCJData: '', // 转盘内容
			}
		},
		mounted() {
			this.cjdata()
		},
		methods: {
			cjdata() { // 请求数据
				this.resCJData = [
					{
						id: "1",
						name: "宝箱1宝箱1宝箱1宝箱1",
						image: "../../static/golang.png",
					},
					{
						id: "1",
						name: "宝箱2宝箱2宝箱2",
						image: "../../static/golang.png",
					},
					{
						id: "1",
						name: "宝箱3宝箱3宝箱3",
						image: "../../static/golang.png",
					},
					{
						id: "1",
						name: "宝箱4宝箱4宝箱4宝箱4",
						image: "../../static/golang.png",
					},
					{
						id: "1",
						name: "宝箱5宝箱5宝箱5",
						image: "../../static/golang.png",
					},
					{
						id: "1",
						name: "宝箱6宝箱6宝箱6宝箱6",
						image: "../../static/golang.png",
					},
				]
			},
			cjReq() {	//  点击抽奖
				if (this.cjName == ''){ // 节流 (不允许点击)
					this.cjName = getRandomIntInclusive(1,6) // 无数据，生成随机数
					function getRandomIntInclusive(min, max) {
					  min = Math.ceil(min);
					  max = Math.floor(max);
					  return Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值 
					}
					console.log("中奖：",this.cjName)
					/* // 根据后端返回，查找id 返回下标用于位置
					this.cjName = find()
					function find(){ 
						let index = 1
						for (let v of this.resCJData) {
							if (res.data.data.lottery_id == v.id) {
								return index
							}
							index++
						}
					}
					*/
				   
					// 抽奖旋转完毕
					setTimeout(()=>{
						this.cjName = ''  // 允许点击
						console.log("还原")
					},3000)
				}
				
			}
		},
		computed: {

		}
	}
</script>

<style lang="scss">
	// 左上角
	@keyframes cjicon {
		0% {
			transform: scale(1);
		}

		,
		100% {
			transform: scale(1.3);
		}
	}
	// 左上角
	.left_top{
		z-index: 90;animation: cjicon alternate infinite 1s ;-webkit-animation: cjicon alternate infinite 1s ;position: absolute;top: 50px;left: 7px;background: url(../../static/indexz.png) no-repeat;background-size: 100% 100%;border-radius: 200px;width: 50px;height: 50px;
	}
	// 基于定位
	.turn{
		animation: forwards 2s;
		-webkit-animation: forwards 2s ;
		width: 300px;
		height: 300px;
		position: relative;
		border-radius: 1000px;
	}
	// 由于-webkit-选择了绑定class，微信小程序可以选择绑定style ( :style="{'animation-name' : 'cjstar' + cjName }" )
	.cjstar1{
		animation-name:cjstar1;
		-webkit-animation-name:cjstar1;
	}
	.cjstar2{
		animation-name:cjstar2;
		-webkit-animation-name:cjstar2;
	}
	.cjstar3{
		animation-name:cjstar3;
		-webkit-animation-name:cjstar3;
	}
	.cjstar4{
		animation-name:cjstar4;
		-webkit-animation-name:cjstar4;
	}
	.cjstar5{
		animation-name:cjstar5;
		-webkit-animation-name:cjstar5;
	}
	.cjstar6{
		animation-name:cjstar6;
		-webkit-animation-name:cjstar6;
	}
	
	// 内容样式
	.cjItemStyle {
		color: #FF512F;
		font-size: 12px;
		text-align: center;
		overflow: hidden;
		//超出的文本隐藏
		text-overflow: ellipsis;
		//溢出用省略号显示
		display: -webkit-box;
		//将对象作为弹性伸缩盒子模型显示。
		-webkit-box-orient: vertical;
		//从上到下垂直排列子元素（设置伸缩盒子的子元素排列方式）
		-webkit-line-clamp: 2;
		//这个属性不是css的规范属性，需要组合上面两个属性，表示显示的行数。
		display: flex;
		flex-flow: column;
		justify-content: center;
		align-items: center;
		width: 80px;
		height: 80px;
	}
	// 内容定位
	.cj-item0 {
		position: absolute;
		top: 33px;
		    left: 109px;
	}

	.cj-item1 {
		position: absolute;
		top: 69px;
		    right: 47px;
		transform: rotate(60deg);
	}

	.cj-item2 {
		position: absolute;
		    top: 143px;
		    right: 47px;
		transform: rotate(120deg);
	}

	.cj-item3 {
		position: absolute;
		top: 186px;
		right: 111px;
		transform: rotate(180deg);
	}

	.cj-item4 {
		position: absolute;
		    top: 142px;
		    left: 45px;
		transform: rotate(240deg);
	}

	.cj-item5 {
		position: absolute;
		    top: 69px;
		    left: 46px;
		transform: rotate(300deg);
	}
	// 内容动画
	@keyframes cjstar1 {
		0% {
			transform: rotate(0deg);
		},
		100% {
			transform: rotate(3600deg);
		}
	}

	@keyframes cjstar2 {
		0% {
			transform: rotate(0deg);
		},
		100% {
			transform: rotate(3540deg);
		}
	}

	@keyframes cjstar3 {
		0% {
			transform: rotate(0deg);
		},
		100% {
			transform: rotate(3480deg);
		}
	}

	@keyframes cjstar4 {
		0% {
			transform: rotate(0deg);
		},
		100% {
			transform: rotate(3420deg);
		}
	}

	@keyframes cjstar5 {
		0% {
			transform: rotate(0deg);
		},
		100% {
			transform: rotate(3360deg);
		}
	}

	@keyframes cjstar6 {
		0% {
			transform: rotate(0deg);
		},
		100% {
			transform: rotate(3300deg);
		}
	}
</style>
