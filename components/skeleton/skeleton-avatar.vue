<template>
	<view class="mei-skeleton-avatar" :class="[shapeClass,sizeClass]"></view>
</template>

<script>
	export default {
		name: 'meiSkeletonAvatar',
		props: {
			shape: {
				type: String,
				default: 'circle'
			},
			size: {
				type: String,
				default: 'small'
			}
		},
		computed: {
			shapeClass(){
				return `mei-skeleton-avatar--${this.shape}`
			},
			sizeClass(){
				return `mei-skeleton-avatar--${this.size}`
			},
		},
		data() {
			return {
			};
		}
	}
</script>

<style lang="scss">
.mei-skeleton-avatar {
  display: inline-block;
  vertical-align: top;
  background: #f2f2f2;
}
.mei-skeleton-avatar--small {
  width: 80upx;
  height: 80upx;
  line-height: 80upx
}
.mei-skeleton-avatar--large {
  width: 96upx;
  height: 96upx;
  line-height: 96upx
}
.mei-skeleton-avatar--circle {
  border-radius: 50%
}
.mei-skeleton-avatar--rounded {
  border-radius: 8upx
}
.mei-skeleton-avatar--square {
  border-radius: 0
}
.active .mei-skeleton-avatar{
  background: linear-gradient(90deg,#f2f2f2 25%,#e6e6e6 37%,#f2f2f2 63%);
  animation: loading 1.4s ease infinite;
  background-size: 400% 100%
}
@keyframes loading {
  0% {
    background-position: 100% 50%
  }
  100% {
    background-position: 0 50%
  }
}
</style>
