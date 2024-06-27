<template>
	<div class="text-tags">
		<v-row class="text-tags__row" ref="wrapper" :class="alignmentClass">
			<v-col v-for="(tag, index) in tags" :key="index" :ref="`tag-${index}`" class="text-tags__tag"
				:class="{ 'is-hide': isVisible(index) == false }">
				<v-icon class="text-tags__icon">{{ tag?.icon || 'mdi-circle-small' }}</v-icon>
				<span>{{ tag.text || '' }}</span>
			</v-col>
		</v-row>
	</div>
</template>

<script>
export default {
	name: "TextTags",
	props: {
		tags: {
			type: Array,
			required: true,
		},
		alignment: {
			type: String,
			default: "left",
			validator: value => ["left", "justify"].includes(value),
		},
	},
	data() {
		return {
			hideIndices: [],
			resizeTimeout: null,
		};
	},
	computed: {
		alignmentClass() {
			return this.alignment === "justify" ? "text-tags--justify" : "text-tags--left";
		},
	},
	methods: {
		calculateVisibleTags() {
			this.hideIndices = [];

			this.$nextTick(() => {
				const wrapperWidth = this.$refs.wrapper.offsetWidth;
				let totalWidth = 0;
				
				for (let index = 0; index < this.tags.length; index++) {
					const tagEl = this.$refs[`tag-${index}`][0];
					const tagWidth = tagEl ? tagEl.offsetWidth : 0;
					
					if (totalWidth + tagWidth > wrapperWidth){
						this.hideIndices.push(index);
					}
					totalWidth += tagWidth;
				}
			});
		},
		isVisible(index) {
			return !this.hideIndices.includes(index);
		},
		handleResize() {
			clearTimeout(this.resizeTimeout);
			this.resizeTimeout = setTimeout(this.calculateVisibleTags, 100);
		},
	},
	mounted() {
		this.calculateVisibleTags();
		window.addEventListener("resize", this.handleResize);
	},
	beforeDestroy() {
		window.removeEventListener("resize", this.handleResize);
	},
	watch: {
		tags() {
			this.calculateVisibleTags();
		},
	},
};
</script>

<style scoped lang="scss">
.text-tags {
	&__row {
		display: flex;
		flex-wrap: nowrap;
		align-items: stretch;
		margin: 0;
		overflow: hidden;
	}

	&--left {
		justify-content: flex-start;
	}

	&--justify {
		justify-content: space-between;
	}

	&__tag {
		display: flex;
		align-items: center;
		padding: 0;
		flex: 0 1 auto;
		width: auto;

		&.is-hide {
			display: none;
		}

		&:first-child {
			.text-tags__icon {
				display: none;
			}
		}
	}

	&__icon {
		margin-right: 4px;
	}
}
</style>