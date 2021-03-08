<template>
	<div class="popup__wrapper">
		<form class="popup__inner">
			<div class="popup__content">
				<div class="popup__content-item">
					<label class="popup__label">
						<div>
							<span>старое название:</span> {{ popup_item.name }}
						</div>
						<input type="text" name="name" />
					</label>
				</div>

				<dir class="popup__content-item">
					<label class="popup__label">
						<div>
							<span>старое описание:</span>
							{{ popup_item.description }}
						</div>
						<input type="text" name="description" />
					</label>
				</dir>

				<button class="popup__btn" type="submit">Изменить</button>
			</div>
			<div @click="closePopup" class="popup__close">X</div>
		</form>
	</div>
</template>

<script>
export default {
	name: 'v-popup',
	props: {
		popup_item: {
			type: Object,
			default() {
				return {};
			},
		},
	},
	data: () => ({}),

	methods: {
		closePopup() {
			this.$emit('closePopup');
		},
	},

	computed: {},
};
</script>

<style lang="sass"></style>
