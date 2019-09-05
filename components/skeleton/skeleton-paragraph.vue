<template>
	<view class="mei-skeleton-paragraph" :class="[rounded? 'mei-skeleton-paragraph--rounded':'']">
		<block v-for="(row,index) in rows" :key="index">
			<view class="mei-skeleton-paragraph__row"></view>
		</block>
	</view>
</template>

<script>
	export default {
		name: 'meiSkeletonParagraph',
		props: {
			rows: {
				type: Number,
				default: 4
			},
			rounded: {
				type: Boolean,
				value: true,
			},
			
		},
		data() {
			return {

			};
		}
	}
</script>

<style>
	.mei-skeleton-paragraph {
		position: relative;
	}

	.mei-skeleton-paragraph__row {
		height: 32upx;
		background: #f2f2f2;
		width: 100%;
		margin-top: 32upx
	}

	.mei-skeleton-paragraph__row:first-child {
		margin-top: 0
	}

	.mei-skeleton-paragraph__row:nth-child(4n+1) {
		width: 80%
	}

	.mei-skeleton-paragraph__row:nth-child(4n+2) {
		width: 100%
	}

	.mei-skeleton-paragraph__row:nth-child(4n+3) {
		width: 70%
	}

	.mei-skeleton-paragraph__row:nth-child(4n+4) {
		width: 85%
	}

	.mei-skeleton-paragraph--rounded .mei-skeleton-paragraph__row {
		border-radius: 8upx
	}

	.active .mei-skeleton-paragraph__row {
		background: linear-gradient(90deg, #f2f2f2 25%, #e6e6e6 37%, #f2f2f2 63%);
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
