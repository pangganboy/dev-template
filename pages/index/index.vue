<template>
	<view>
		<view class="sys-head" :style="{marginTop:margin_top + 'px',height:sys_height + 'px'}">
		</view>
		<view class="main">

		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				margin_top: 0,
				height: 0,
			}
		},
		onReady() {
			let that = this;
			let data = uni.getMenuButtonBoundingClientRect();
			that.margin_top = data.top;
			that.sys_height = data.height;
			console.log('that.sys_height', that.sys_height)
			uni.getSystemInfo({
				success(res) {
					console.log('sysInfo', res)
					// that.margin_top = res.statusBarHeight;

				}
			});
			console.log('ButtonBound', data);
			const query = uni.createSelectorQuery().in(this);
			const menuButton = uni.getMenuButtonBoundingClientRect();
			query.select('.sys-head').boundingClientRect(data => {
				console.log('sys-head', data)
			}).exec();


			uni.getSystemInfo({
				success: e => {
					let StatusBar = e.statusBarHeight;
					let rect = wx.getMenuButtonBoundingClientRect();
					if (e.system.toLowerCase().indexOf('ios') > -1) {
						//IOS  
						let CustomBar = rect.bottom + (rect.top - e.statusBarHeight) * 2;
						let HeaderBar = CustomBar - e.statusBarHeight;
						console.log(CustomBar,HeaderBar)
					} else {
						//安卓  
						let HeaderBar = rect.height + (rect.top - e.statusBarHeight) * 2;
						let CustomBar = HeaderBar + e.statusBarHeight;
						console.log(CustomBar,HeaderBar)
					}
				}
			});
		}
	}
</script>
<style lang="scss">
	page {
		height: 100%;
	}

	.sys-head {
		width: 100%;
	}

	.main {
		height: 400rpx;
		background-color: var(--view-default-background);
	}
</style>