<!--
 * @Author: cully fung
 * @Date: 2021-08-01 21:15:46
 * @LastEditTime: 2022-08-29 23:22:40
 * @LastEditors: cully fung
 * @Description:
-->
<template>
	<div>
		<!-- 官方榜单 -->
		<div>
			<h1 class="font-medium cursor-default mb-5">官方榜</h1>
			<rank-item
				v-for="item in officialRank"
				:key="item.id"
				:id="item.id"
			></rank-item>
		</div>
		<!-- 全球榜 -->
		<div>
			<h1 class="title">全球榜</h1>
			<div class="grid grid-cols-6 gap-4">
				<router-link
					v-for="item in globalRank"
					:key="item.id"
					:to="{
						path: '/songlist',
						query: {
							id: item.id
						}
					}"
				>
					<playlist-item
						:src="item.coverImgUrl"
						:label="item.name"
						:num="item.playCount"
						position="center"
					></playlist-item>
				</router-link>
			</div>
		</div>
	</div>
</template>

<script>
import RankItem from '@/components/rank-item'
import PlaylistItem from '@/components/playlist-item'
import { getToplist } from '@/api'

export default {
	name: 'Rank',
	components: {
		RankItem,
		PlaylistItem
	},
	computed: {
		officialRank() {
			return this.toplist.filter(item => !!item.ToplistType)
		},
		globalRank() {
			return this.toplist.filter(item => !item.ToplistType)
		}
	},
	data() {
		return {
			toplist: [],
			artistToplist: {}
		}
	},

	methods: {
		// 获取排行榜
		async getTopList() {
			const res = await getToplist()
			if (res.code !== 200) {
				return this.$notify.error('获取排行榜失败！')
			}
			this.toplist = res.list
			this.artistToplist = res.artistToplist
		}
	},
	created() {
		this.getTopList()
	}
}
</script>
