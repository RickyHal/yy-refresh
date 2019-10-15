<template>
	<loading @loading="onloading" @pullingup="onpullingup" :style="{width:screenWidth}"  class="load-more-div"  :display="showLoadMore ? 'show' : 'hide'">
		<image :src="loadingIcon[loadMoreStatus]" class="loading-icon"></image>
		<text class="load-more-div-text">{{ loadingText[loadMoreStatus] }}</text>
	</loading>
</template>

<script>
export default {
	props:{
		loadingText: {
			type:Array,
			default:['加载更多', '松开加载', '加载中...', '加载完成']
		}
	},
	data() {
		return {
			loadMoreStatus: 0,
			showLoadMore: false,
			screenWidth:750,
			loadingIcon: [
				'../../static/yy-refresh/arrow-down.png',
				'../../static/yy-refresh/arrow-up.png',
				'../../static/yy-refresh/loading.gif',
				'../../static/yy-refresh/refresh-ok.png'
			]
		};
	},
	created() {
		this.screenWidth=uni.getSystemInfoSync().windowWidth;
	},
	methods: {
		onpullingup(event) {
			this.showLoadMore = true;
			var refreshHeight = event.viewHeight;
			var pullingDistance = event.pullingDistance;
			if (refreshHeight < pullingDistance) {
				this.loadMoreStatus = 1;
			} else {
				this.loadMoreStatus = 0;
			}
		},
		onloading() {
			this.loadMoreStatus = 2;
			this.$emit('loadMore');
		},
		finish(time) {
			var that = this;
			that.loadMoreStatus = 3;
			setTimeout(function() {
				that.showLoadMore = false;
			}, time);
		}
	}
};
</script>

<style>
.load-more-div {
	height: 60px;
	flex-direction: row;
	justify-content: center;
	align-items: center;
}

.loading-icon {
	width: 16px;
	height: 16px;
}

.load-more-div-text {
	font-size: 14px;
	color: #999;
	line-height: 60px;
	text-align: center;
	margin-left: 5px;
}
</style>
