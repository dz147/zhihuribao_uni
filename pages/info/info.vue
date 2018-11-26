<template>
	<view>
		<view class="content">
			<view class="title">
				{{title}}
			</view>
			<view class="">
				<rich-text class="richText" :nodes="strings" ></rich-text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '',
				strings: ''
			};
		},
		onLoad:function(e) {
			console.log(e.newsid);
			uni.request({
				url: 'http://news-at.zhihu.com/api/4/news/'+e.newsid,
				method: 'GET',
				data: {},
				success: res => {
					this.title = res.data.title;
					this.strings = res.data.body.replace("type=“text/javascript”",'type="text/javascript"');
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
	.content{padding: 10upx %2; width: 96%; flex-wrap:wrap ;}
	.title{line-height: 2em; font-weight: 700;font-size: 30upx;}
	.art-content{line-height: 2em;font-size: 18upx;}
</style>
