<!--
 * @Author: cully fung
 * @Date: 2021-08-24 17:13:00
 * @LastEditTime: 2022-08-28 23:58:16
 * @LastEditors: cully fung
 * @Description:
-->
<template>
	<div class="song-list">
		<slot>
			<song-list-item
				v-for="(item, index) in list"
				:key="item.id"
				:song="item"
				:index="index"
				class="song-list-item"
			></song-list-item>
		</slot>
	</div>
</template>

<script>
import SongListItem from './song-list-item'
export default {
	components: {
		SongListItem
	},
	props: {
		list: {
			type: Array,
			required: true
		}
	}
}
</script>

<style scoped>
.song-list {
	@apply px-4 py-2;
}
.song-list .song-list-item:nth-child(even) {
	@apply bg-gray-50;
}
.song-list .song-list-item {
	@apply hover:bg-gray-100;
}
</style>
