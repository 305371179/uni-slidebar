<template>
	<view class="container">
		<view class="skeleton-container" v-if="!hideSkeleton">
			<block v-for="item in 5" :key="item">
				<mei-skeleton active>
				<mei-skeleton-avatar></mei-skeleton-avatar>
				<mei-skeleton-paragraph class="mei-flex-1"></mei-skeleton-paragraph>
			</mei-skeleton>
			</block>
		</view>
		<scroll-view scroll-y scroll-with-animation class="tab-view" :scroll-top="scrollTop">
			<view v-for="(item,index) in tabbar" :id="'tab'+index" :key="index" class="tab-bar-item" :class="[currentTab==index ? 'active' : '']"
			 :data-current="index" @tap.stop="swichNav">
				<text>{{item}}</text>
			</view>
		</scroll-view>
		<view class="right-box">
			<!--  -->
			<view style="position:relative;width:100%:">
				<view class="sticky-header sticky-header--fixed">
					{{currentItem}}
				</view>
			</view>
			<scroll-view class="right-scroll" :scroll-into-view="headerViewId" scroll-y scroll-with-animation :scrollTop="rightScrollTop"
			 @scroll="rightScroll">
				<view v-for="(item,index) in tabbar" :key="index" :id="'header'+index">
					<view class="sticky-header" :class="[currentTab === index ? 'sticky-header--hidden':'']">
						{{item}}
					</view>
					<view class="page-view">
						<swiper indicator-dots autoplay circular :interval="5000" :duration="150" class="swiper">
							<swiper-item @tap.stop="detail">
								<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/mall/banner/2.jpg"
								 class="slide-image" />
							</swiper-item>
							<swiper-item @tap.stop="detail">
								<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/mall/banner/4.jpg"
								 class="slide-image" />
							</swiper-item>
							<swiper-item @tap.stop="detail">
								<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/mall/banner/5.jpg"
								 class="slide-image" />
							</swiper-item>
						</swiper>
						<view class="class-box">
							<view class="class-item">
								<view class="class-name">推荐分类</view>
								<view class="g-container">
									<view class="g-box" @tap.stop="productList" data-key="高价回收">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/11.jpg"
										 class="g-image" />
										<view class="g-title">高价回收</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="好物优选">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/22.jpg"
										 class="g-image" />
										<view class="g-title">好物优选</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="iphone X">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/33.jpg"
										 class="g-image" />
										<view class="g-title">iphone X</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="电动牙刷">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/44.jpg"
										 class="g-image" />
										<view class="g-title">电动牙刷</view>
									</view>
								</view>
							</view>

							<view class="class-item">
								<view class="class-name">专场推荐</view>
								<view class="g-container">
									<view class="g-box" @tap.stop="productList" data-key="笔记本">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/11.jpg"
										 class="g-image" />
										<view class="g-title">笔记本</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="电水壶">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/22.jpg"
										 class="g-image" />
										<view class="g-title">电水壶</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="iphone X">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/33.jpg"
										 class="g-image" />
										<view class="g-title">iphone X</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="电动牙刷">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/44.jpg"
										 class="g-image" />
										<view class="g-title">电动牙刷</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="抽纸">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/55.jpg"
										 class="g-image" />
										<view class="g-title">抽纸</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="笔记本">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/11.jpg"
										 class="g-image" />
										<view class="g-title">笔记本</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="电水壶">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/22.jpg"
										 class="g-image" />
										<view class="g-title">电水壶</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="iphone X">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/33.jpg"
										 class="g-image" />
										<view class="g-title">iphone X</view>
									</view>
								</view>
							</view>

							<view class="class-item">
								<view class="class-name">专场推荐</view>
								<view class="g-container">
									<view class="g-box" @tap.stop="productList" data-key="iphone X">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/33.jpg"
										 class="g-image" />
										<view class="g-title">iphone X</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="电动牙刷">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/44.jpg"
										 class="g-image" />
										<view class="g-title">电动牙刷</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="抽纸">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/55.jpg"
										 class="g-image" />
										<view class="g-title">抽纸</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="笔记本">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/11.jpg"
										 class="g-image" />
										<view class="g-title">笔记本</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="电水壶">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/22.jpg"
										 class="g-image" />
										<view class="g-title">电水壶</view>
									</view>
									<view class="g-box" @tap.stop="productList" data-key="iphone X">
										<mei-lazy-img :scroll="scroll" :box="scrollBox" src="../../static/images/product/33.jpg"
										 class="g-image" />
										<view class="g-title">iphone X</view>
									</view>
								</view>
							</view>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>

	</view>
</template>

<script>
	import meiSkeleton from '../../components/skeleton/skeleton.vue'
	import meiSkeletonAvatar from '../../components/skeleton/skeleton-avatar.vue'
	import meiSkeletonParagraph from '../../components/skeleton/skeleton-paragraph.vue'
	import meiLazyImg from '../../components/lazy-img/lazy-img.vue'
	export default {
		components: {
			meiLazyImg,
			meiSkeleton,
			meiSkeleton,
			meiSkeletonAvatar,
			meiSkeletonParagraph
		},
		data() {
			return {
				hideSkeleton: false,
				tabbar: ["推荐分类", "进口超市", "国际名牌", "奢侈品", "海囤全球", "男装", "女装", "男鞋", "女鞋", "钟表珠宝", "手机数码", "电脑办公", "家用电器", "玩具乐器",
					"运动户外", "宠物生活", "特产馆"
				],
				currentTab: 0, //预设当前项的值
				scrollTop: 0, //tab标题的滚动条位置
				rightScrollTop: 0,
				tabScrollInfo: {
					scrollHeight: 0,
					scrollTop: 0
				},
				rightScrollInfo: {
					scrollHeight: 0,
					scrollTop: 0
				},
				stickyScrollTop: 0,
				headerViewId: '',
				tabView: '',
				tabHeight: '',
				// caches:{},
				// lastScrollTop: false,
				scrollBox: null,
				scroll: {
					scrollLeft: 0,
					scrollTop: 0
				}

			}
		},
		onLoad: function(options) {

		},
		computed: {
			currentItem() {
				const item = this.tabbar[this.currentTab]
				if (!item) {
					return {}
				}
				return item
			}
		},
		mounted() {
			setTimeout(()=>{
				this.hideSkeleton = true
			},2000)
			this.init()
			uni.onWindowResize((res) => {
				this.init()
			})
		},
		beforeDestroy() {
			uni.offWindowResize(() => {
				console.log('取消监听窗口尺寸变化事件')
			})
		},
		methods: {
			init() {
				const query = uni.createSelectorQuery().in(this)
				const tabView = query.select('.tab-view')
				this.tabViewHeight = 0
				this.tabbar.length && tabView.boundingClientRect((res) => {
					if (res) {
						this.tabViewHeight = res.height
					}
				}).exec()
				this.tabbar.length && query.select('#tab0').boundingClientRect((res) => {
					if (res) {
						this.tabHeight = res.height
					}
				}).exec()
				query.select('.right-scroll').boundingClientRect((res) => {
					if (res) {
						this.scrollBox = {
							left: res.left,
							top: res.top,
							width: res.width,
							height: res.height
						}
					}
				}).exec()
			},
			rightScroll(e) {
				clearTimeout(this.lazyId)
				this.lazyId = setTimeout(() => {
					this.scroll = {
						scrollLeft: e.target.scrollLeft || 0,
						scrollTop: e.target.scrollTop || 0,
					}
				}, 200)

				this.rightScrollInfo = e.target
				if (this.isScroll) return this.isScroll = false
				const query = uni.createSelectorQuery().in(this)
				const headerIndex = this.currentTab
				const headerId = 'header' + headerIndex
				const header = query.select('#' + headerId)
				header && header.boundingClientRect((res) => {
					if (!res) return
					const height = res.height
					const top = res.top
					//已经向上滚动，离开了显示区，显示下一个
					if (top < -height) {
						return this.setCurrentTab(this.currentTab + 1)
					}
					if (top > 0) {
						return this.setCurrentTab(this.currentTab - 1)
					}
				}).exec()
			},
			setCurrentTab(index) {
				if (index < 0 || index >= this.tabbar.length) {
					return
				}
				this.currentTab = index
				this.headerViewId = ''
				this.tabViewId = 'tab' + index
				this.setTabToCenter()

				// header.boundingClientRect((res) => {
				// 	if (res) {
				// 		const scrollHeight = this.rightScrollInfo.scrollHeight
				// 		const scrollTop = this.rightScrollInfo.scrollTop
				// 		const currentTabHeight = res.height
				// 		const currentTabTop = res.top
				// 		const center = this.tabHeight/2 -(currentTabTop +currentTabHeight/2)
				// 		this.rightScrollTop = scrollTop + currentTabTop 
				// 		this.isScroll = true
				// 		// console.log(this.rightScrollTop)
				// 	}
				// }).exec()
			},
			tabScroll(e) {
				this.tabScrollInfo = e.target
			},
			// 点击标题切换当前页时改变样式
			swichNav: function(e) {

				this.isScroll = true
				const cur = parseInt(e.currentTarget.dataset.current)
				this.currentTab = cur
				this.headerViewId = 'header' + cur
				this.tabViewId = 'tab' + cur
				this.setTabToCenter()
			},
			setTabToCenter() {
				if (!this.tabbar.length) return
				const scrollHeight = this.tabScrollInfo.scrollHeight
				const scrollTop = this.tabScrollInfo.scrollTop
				const currentTabHeight = this.tabHeight
				const currentTabTop = this.currentTab * currentTabHeight - scrollTop
				const center = this.tabViewHeight / 2 - (currentTabTop + currentTabHeight / 2)
				this.scrollTop = scrollTop - center
			},
			detail(e) {},
			productList(e) {}
		}
	}
</script>

<style>
	@import '../../components/style/meiui.css';
	.skeleton-container{
		background: white;
		width: 100%;
		height:100%;
		overflow: hidden;
		position:absolute;
		left:0;
		top:0;
		z-index: 1000;
	}
	.mei-skeleton{
		padding: 40upx 8upx;
	}
	.mei-skeleton-avatar{
		margin: 20upx;
	}
	
	.active .mei-skeleton-avatar,
	.active .mei-skeleton-paragraph__row {
		background: linear-gradient(90deg, #f2f2f2 25%, #e6e6e6 37%, #f2f2f2 63%);
		animation: loading 1.4s ease infinite;
		background-size: 400% 100%
	}
	page {
		background: #fcfcfc;
		height: 100%;
	}

	uni-page-body,
	uni-page-refresh {
		height: 100%;
	}

	/* 左侧导航布局 start*/

	/* 隐藏scroll-view滚动条*/

	::-webkit-scrollbar {
		width: 0;
		height: 0;
		color: transparent;
	}

	.container {
		display: flex;
		height: 100%;
	}

	.tab-view {
		height: 100%;
		width: 200upx;
		z-index: 10;
	}

	.tab-bar-item {
		width: 200upx;
		height: 110upx;
		background: #f6f6f6;
		box-sizing: border-box;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 26upx;
		color: #444;
		font-weight: 400;
	}

	.tab-view .active {
		position: relative;
		color: #000;
		font-size: 30upx;
		font-weight: 600;
		background: #fcfcfc;
	}

	.tab-view .active::before {
		content: "";
		position: absolute;
		border-left: 8upx solid #E41F19;
		height: 30upx;
		left: 0;
	}

	/* 左侧导航布局 end*/

	.right-box {
		width: 100%;
		height: 100%;
		position: absolute;
		padding-left: 220upx;
		box-sizing: border-box;
		left: 0;
	}

	.right-scroll {
		height: 100%;
	}

	.sticky-header {
		height: 50px;
		line-height: 50px;
		background: white;
	}

	.sticky-header--fixed {
		will-change: transform;
		transform: translate3d(0, 0, 0);
		position: absolute;
		width: 100%;

		/* left:0;
		top:44px;
		right:0; */
		z-index: 2;
	}

	.sticky-header--absolute {
		position: absolute;
		bottom: 0;
	}

	.sticky-header--hidden {
		visibility: hidden;
	}

	.page-view {
		width: 100%;
		overflow: hidden;
		padding-top: 20upx;
		padding-right: 20upx;
		box-sizing: border-box;
		padding-bottom: env(safe-area-inset-bottom);
	}

	.swiper {
		width: 100%;
		height: 220upx;
		border-radius: 12upx;
		overflow: hidden;
		transform: translateZ(0);
	}

	/* #ifdef APP-PLUS || MP */
	.swiper .wx-swiper-dot {
		width: 8upx;
		height: 8upx;
		display: inline-flex;
		background: none;
		justify-content: space-between;
	}

	.swiper .wx-swiper-dot::before {
		content: '';
		flex-grow: 1;
		background: rgba(255, 255, 255, 0.8);
		border-radius: 16upx;
		overflow: hidden;
	}

	.swiper .wx-swiper-dot-active::before {
		background: #fff;
	}

	.swiper .wx-swiper-dot.wx-swiper-dot-active {
		width: 16upx;
	}

	/* #endif */

	/* #ifdef H5 */
	.swiper .uni-swiper-dot {
		width: 8rpx;
		height: 8rpx;
		display: inline-flex;
		background: none;
		justify-content: space-between;
	}

	.swiper .uni-swiper-dot::before {
		content: '';
		flex-grow: 1;
		background: rgba(255, 255, 255, 0.8);
		border-radius: 16rpx;
		overflow: hidden;
	}

	.swiper .uni-swiper-dot-active::before {
		background: #fff;
	}

	.swiper .uni-swiper-dot.uni-swiper-dot-active {
		width: 16rpx;
	}

	/* #endif */

	.slide-image {
		width: 100%;
		height: 220upx;
	}

	.class-box {
		padding-top: 30upx;
	}

	.class-item {
		background: #fff;
		width: 100%;
		box-sizing: border-box;
		padding: 20upx;
		margin-bottom: 20upx;
		border-radius: 12upx;
	}

	.class-name {
		font-size: 22upx;
	}

	.g-container {
		/* padding-top: 20upx; */
		display: flex;
		display: -webkit-flex;
		justify-content: flex-start;
		flex-direction: row;
		flex-wrap: wrap;
	}

	.g-box {
		width: 33.3333%;
		text-align: center;
		padding-top: 40upx;
	}

	.g-image,
	.mei-lazy-img-image {
		width: 120upx;
		height: 120upx;
	}

	.g-title {
		font-size: 22upx;
	}
</style>
