<template>
	<div id="app">
		<div class="main">
			<div class="main__inner" v-cloak>
				<ul class="deck">
					<card
						v-for="(item, index) in info"
						:key="item.id"
						:card_item="item"
						:index="index"
						@deleteItem="deleteItem"
					/>
				</ul>

				<div>
					<button
						class="btn"
						v-if="info !== null"
						@click="addNewPage"
					>
						SHOW NEXT
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import axios from 'axios';

import card from './components/card';

export default {
	props: {},

	components: {
		card,
	},

	data: () => ({
		beer: [],
		info: null,
		pageNumber: 1,
		res: null,
	}),

	methods: {
		deleteItem(index) {
			this.info.splice(index, 1);
		},

		async getDataBase() {
			await axios
				.get(
					`https://api.punkapi.com/v2/beers?page=${this.pageNumber}&limit=25`
				)
				.then((response) => (this.beer = response.data));

			return this.beer;
		},

		async addNewPage() {
			this.pageNumber++;

			await this.getDataBase();

			this.info = this.info.concat(this.beer);
		},
	},
	computed: {},

	mounted() {
		axios
			.get('https://api.punkapi.com/v2/beers?page=1&limit=25')
			.then((response) => (this.info = response.data));
	},
};
</script>

<style lang="sass">
@import './assets/style'
</style>
