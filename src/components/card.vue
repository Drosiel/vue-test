<template>
	<li class="card">
		<v-popup
			v-if="IsEditPopupVisible"
			@closePopup="closeEditPopup"
			:popup_item="card_item"
		>
		</v-popup>

		<div class="card__inner">
			<div class="card__id">{{ card_item.id }}</div>
			<div class="card__name">{{ card_item.name }}</div>
			<div class="card__img">
				<img :src="card_item.image_url" alt="" />
			</div>
			<div class="card__description">
				{{ card_item.description }}
			</div>
			<div class="card__tips">
				{{ card_item.brewers_tips }}
			</div>
			<div class="card__btn">
				<button @click="editItem()" class="card__edit">
					Edit
				</button>
				<button @click="deleteItem(index)" class="card__delete">
					Delete
				</button>
			</div>
		</div>
	</li>
</template>

<script>
import vPopup from './popup/popup';

export default {
	name: 'card',

	props: {
		card_item: {
			type: Object,
			default() {
				return {};
			},
		},
		index: Number,
	},

	components: {
		vPopup,
	},

	data: () => ({
		IsEditPopupVisible: false,
	}),

	methods: {
		editItem() {
			this.IsEditPopupVisible = true;
		},

		closeEditPopup() {
			this.IsEditPopupVisible = false;
		},

		deleteItem(index) {
			this.$emit('deleteItem', index);
		},
	},

	computed: {},
};
</script>

<style lang="sass"></style>
