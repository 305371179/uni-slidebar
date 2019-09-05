<template>
	<view class="mei-skeleton" :class="[active?'active':'']">
		<slot></slot>
	</view>
</template>

<script>
	export default {
		name: 'meiSkeleton',
		props:{
			active:{
				type: Boolean,
				default: false
			}
		},
		data() {
			return {
				
			};
		}
	}
</script>

<style>
.mei-skeleton{
		position:relative;
		display: flex;
	}
</style>
