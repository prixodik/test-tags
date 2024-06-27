<template>
	<v-app class="index-page">
		<v-main class="index-page__main">
			<v-container class="index-page__container">
				<div class="index-page__wrapper">
					<text-tags class="index-page__tags index-page__tags--1" :tags="tags" alignment="left" />
				</div>
				<div class="index-page__wrapper">
					<text-tags class="index-page__tags index-page__tags--2" :tags="tags" alignment="justify" />
				</div>
				<v-row class="index-page__row">
					<v-col class="index-page__col" cols="6">
						<div class="index-page__wrapper">
							<text-tags :tags="tags" alignment="left" />
						</div>
					</v-col>
					<v-col class="index-page__col" cols="6">
						<div class="index-page__wrapper">
							<text-tags :tags="tags" alignment="justify" />
						</div>
					</v-col>
				</v-row>
			</v-container>
		</v-main>
	</v-app>
</template>

<script>
import TextTags from "./components/TextTags.vue";

export default {
	name: "App",
	components: {
		TextTags,
	},
	data() {
		return {
			tags: [
				{
					text: "Егорка",
					icon: "mdi-circle-small"
				},
				{
					text: "Иван"
				},
				{
					text: "Сидор"
				},
				{
					text: "Емеля",
					icon: "mdi-book-open-page-variant"
				},
				{
					text: "Тракторина"
				},
				{
					text: "Петя"
				},
				{
					text: "Глеб",
					icon: "mdi-calendar-month"
				},
				{
					text: "Вася"
				},
				{
					text: "Дима"
				},
				{
					text: "Вася"
				}
			]
		};
	},
};
</script>

<style lang="scss">
.index-page {
	padding: 40px 0;
	&__container {
		padding: 0 40px;
	}

	&__wrapper {
		background: #ccc;
		margin-bottom: 24px;

		&:last-child {
			margin-bottom: 0;
		}
	}

	&__row {
		margin: 40px -24px -24px;
	}

	&__col {
		padding: 0 24px;
		margin-bottom: 24px;
	}
}
</style>