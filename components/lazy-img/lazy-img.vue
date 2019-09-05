<template>
	<view class="mei-lazy-img">
		<image class="image" :src="loadingSrc" :mode="mode" v-if="loadingSrc && showLoading" :class="[isSuccess?'mei-lazy-img-loading--hidden':'',]"
		 @transitionend="transitionend" />
		<image class="image" :src="src" :mode="mode" @load="loaded" v-if="isLoad" :class="showClass" @transitionend="transitionend1"/>
		<!-- <image class="mei-lazy-img-loading" :src="loadingSrc" v-if="loadingSrc" :class="[isSuccess?'mei-lazy-img-loading--hidden':'',]"></image> -->
	</view>
</template>

<script>
	export default {
		name: "meiLazyImg",
		props: {
			src: {
				type: String,
				default: ''
			},
			preloadSrc: {
				type: String,
				default: ''
			},
			errorSrc: {
				type: String,
				default: ''
			},
			loadingSrc: {
				type: String,
				default: ''
			},
			mode: {
				type: String,
				default: 'scaleToFill'
			},
			scroll: {
				type: Object,
				default () {
					return {
						scrollLeft: 0,
						scrollTop: 0
					}
				}
			},
			box: {
				type: Object,
				default () {
					return {
						left: 0,
						top: 0,
						width: 0,
						height: 0
					}
				}
			},
		},
		data() {
			return {
				isLoad: false,
				isSuccess: false,
				showLoading: true,
				hideClass: false
			}
		},
		computed: {
			showClass(){
				if(!this.isSuccess){
					return 'mei-lazy-img--hidden'
				}else if(!this.hideClass){
					return 'mei-lazy-img--show'
				}else{
					return ''
				}
			},
			currentSrc() {
				if (this.isLoad) {
					return this.src
				}
				if (this.error) {
					return this.errorSrc
				}
				return this.preloadSrc
			}
		},
		watch: {
			box() {
				this.scrollChange()
			},
			scroll() {
				if (this.isLoad) {
					return
				}
				this.scrollChange()
			}
		},
		methods: {
			transitionend() {
				this.showLoading = false
			},
			transitionend1(){
				this.hideClass = false
			},

			loaded(e) {
				if (this.currentSrc !== this.src) {
					return
				}
				this.isSuccess = true
				this.$emit('load', e)
			},
			isInterect(r1, r2) {
				const x1 = r1.left,
					x2 = r2.left,
					y1 = r1.top,
					y2 = r2.top,
					w1 = r1.width,
					w2 = r2.width,
					h1 = r1.height,
					h2 = r2.height;
				if ((x1 + w1) < x2 || (x2 + w2) < x1 || (y1 + h1) < y2 || (y2 + h2) < y1) {
					return false
				}
				this.isLoad = true
				return true
			},
			getBox(callback) {
				const query = uni.createSelectorQuery().in(this)
				query.select('.mei-lazy-img').boundingClientRect((res) => {
					if (res) {
						callback({
							left: res.left,
							top: res.top,
							width: res.width,
							height: res.height
						})
					}
				}).exec()
			},
			scrollChange() {
				this.getBox((mBox) => {
					this.isInterect(mBox, this.box)
				})
			}
		}
	}
</script>

<style scoped>
	.mei-lazy-img {
		position: relative;
		width:100%;
		height:100%;
	}

	image {
		will-change: transform
	}

	.mei-lazy-img--hidden {
		position: absolute;
		opacity: 0;
		pointer-events: none;
	}

	.mei-lazy-img--show {
		/* opacity: 1; */
		transition: opacity 0.2s;
	}

	.mei-lazy-img-loading--hidden {
		position: absolute;
		opacity: 0;
		transition: opacity 0.2s;
	}
	.image{
		width:100%;
		height:100%;
	}
</style>
