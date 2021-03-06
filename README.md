
# yy-refresh
基于uni-app 的nvue上拉刷新和下拉加载插件 ，可以灵活控制刷新和加载的提示。

插件地址[https://ext.dcloud.net.cn/plugin?id=862](https://ext.dcloud.net.cn/plugin?id=862)
## 插件效果
<a href="https://imgchr.com/i/lOfZRO"><img src="https://s2.ax1x.com/2020/01/15/lOfZRO.md.gif" alt="lOfZRO.gif" border="0" /></a>
## 使用教程

* 导入插件
```JavaScript
//下拉刷新插件
import yyRefresh from '@/components/yy-refresh/yy-refresh.nvue';
//上拉加载插件
import yyLoadMore from '@/components/yy-refresh/yy-load-more.vue';
```

* 声明插件
```JavaScript
    components: {
		yyRefresh,
		yyLoadMore
	}
```

* 使用插件
```Html
<list class="list" :style="{ height: screenHeight, width: screenWidth }">
	<!-- 下拉刷新 -->
	<yy-refresh :refresh-text="refreshText" @refresh="onRefresh" ref="yyRefresh"></yy-refresh>
	<cell v-for="(item, index) in testData" :key="index" class="list-item">
		<text style="line-height: 30px;">{{ item }}</text>
	</cell>
	<!-- 上拉加载 -->
	<yy-load-more :loading-text="loadMoreText" @loadMore="onLoadMore" ref="yyLoadMore"></yy-load-more>
</list>
```
在调用插件的页面实现：
```JavaScript
onRefresh() {
	//此处模拟请求数据 Here the request data is simulated
	setTimeout(() => {
		this.testData = 20
		//结束刷新 stop refreshing
		this.$refs.yyRefresh.finish();
	}, 1000);
},
onLoadMore() {
	//此处模拟请求数据  Here the request data is simulated
	setTimeout(() => {
		//结束加载  stop loading
		if (this.testData > 20) {
			this.$refs.yyLoadMore.finish(false);
		} else {
			this.testData += 10
			this.$refs.yyLoadMore.finish(true);
		}
	}, 1000);
}
```
## 参数说明

|参数|插件名|说明|是否必填|默认值|
|--------|--------|--------|--------|--------|
|refresh-text|yy-refresh|插件的下拉刷新提示文本数组，具体参考默认值|否|['下拉刷新', '释放更新', '刷新中...', '刷新成功']|
|loading-text|yy-load-more|上拉加载提示文本数组，具体参考默认值|否|['', '加载中...', '没有更多啦']|
|ref|yy-refresh，yy-load-more|必填属性，用于结束刷新和加载，其值可以自定义，但是在结束刷新或加载时必须使用this.$refs.\<ref>.finish(500);结束|是||

## 监听事件说明

|事件|插件名|说明|
|--------|--------|--------|
|onRefresh|yy-refresh|下拉刷新事件|
|onLoadMore|yy-load-more|上拉加载事件|

## 其它

```JavaScript
that.$refs.yyRefresh.finish(<Number>);
```
其中的Number为加载完成后显示结果的时间（单位为ms），即上拉加载显示加载完成的时间。
```JavaScript
that.$refs.yyLoadMore.finish(<boolean>);
```
其中的Boolean为是否还有更多数据，默认为True
如有BUG欢迎更正，github地址：[https://github.com/RickyHal/yy-refresh](https://github.com/RickyHal/yy-refresh)
