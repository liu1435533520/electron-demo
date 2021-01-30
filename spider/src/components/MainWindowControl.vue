<!--
 * @Author: your name
 * @Date: 2021-01-06 14:56:55
 * @LastEditTime: 2021-01-30 17:07:32
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \electron-demo\spider\src\components\HelloWorld.vue
-->
<template>
	<!-- <input type="text" v-model="dirPath" />
	<button @click="selectDirPath">选择文件夹</button> -->
	<div class="window-control">
		<button @click="minimize">最小化</button>
		<button @click="restore" v-if="isMaxinize">恢复</button>
		<button @click="maximize" v-if="!isMaxinize">最大化</button>
		<button @click="destroy">关闭</button>
	</div>
</template>

<script>
	// const { dialog } = require('electron').remote
	import { remote } from "electron";
	// const { dialog } = remote;
	import { defineComponent, ref, reactive } from "vue";
	export default defineComponent({
		name: "MainWindowControl",
		setup() {
			// let dirPath = ref("");
			// const selectDirPath = () => {
			// 	dialog
			// 		.showOpenDialog(currentWindow, {
			// 			title: "选择文件夹",
			// 			properties: ["openDirectory"]
			// 		})
			// 		.then(result => {
			// 			let dirName = result.canceled ? "" : result.filePaths[0];
			// 			dirPath.value = dirName.replaceAll("\\", "/");
			// 		})
			// 		.catch(err => {
			// 			console.log(err);
			// 		});
			// };
			let isMaxinize = ref(false);
			let currentWindow = remote.getCurrentWindow();
			let windowBounds = currentWindow.getBounds();
			currentWindow.on("moved", () => {
				windowBounds = currentWindow.getBounds();
			});

			const minimize = () => {
				currentWindow.minimize();
			};
			const maximize = () => {
				isMaxinize.value = true;
				currentWindow.maximize();
				currentWindow.setMovable(false);
			};
			const restore = () => {
				isMaxinize.value = false;
				currentWindow.setBounds(windowBounds);
				currentWindow.setMovable(true);
			};
			const destroy = () => {
				currentWindow.destroy();
			};
			return {
				// dirPath,
				// selectDirPath,
				isMaxinize,
				destroy,
				minimize,
				maximize,
				restore
			};
		}
	});
</script>
<style lang="scss">
	.window-control {
		background-color: rgba(255, 255, 255, 0.5);
		-webkit-app-region: drag;
		button {
			-webkit-app-region: no-drag;
		}
	}
</style>