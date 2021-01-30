<!--
 * @Author: your name
 * @Date: 2021-01-06 14:56:55
 * @LastEditTime: 2021-01-30 16:06:25
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \electron-demo\spider\src\App.vue
-->
<template>
	<MainWindowControl />
</template>

<script>
	import MainWindowControl from "./components/MainWindowControl.vue";

	export default {
		name: "App",
		components: {
			MainWindowControl
		}
	};
</script>
<style lang="scss">
	body {
		background-color: #fff;
		resize: none;
	}
</style>