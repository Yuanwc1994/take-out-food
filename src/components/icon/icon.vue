<template>
	<span class="icon" :class="[size,classMap[type]]"></span>
</template>

<script type="text/ecmascript-6">
	export default {
		props: {
			size: {
				type: String,
				default: 'small'
			},
			type: {
				type: Number,
				required: true
			}
		},
		created() {
			this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
		}

	};
</script>

<style lang="scss" rel="stylesheet/scss">
	@import "../../common/styles/mixin.scss";

	.icon {
		display: inline-block;
		vertical-align: top;
		background-repeat: no-repeat;
	}

	.small {
		width: 12px;
		height: 12px;
		background-size: 12px 12px;
		&.decrease {
			@include bg-image('decrease_1');
		}
		&.discount {
			@include bg-image('discount_1');
		}
		&.guarantee {
			@include bg-image('guarantee_1');
		}
		&.invoice {
			@include bg-image('invoice_1');
		}
		&.special {
			@include bg-image('special_1');
		}
	}

	.normal {
		width: 16px;
		height: 16px;
		background-size: 16px 16px;
		&.decrease {
			@include bg-image('decrease_2');
		}
		&.discount {
			@include bg-image('discount_2');
		}
		&.guarantee {
			@include bg-image('guarantee_2');
		}
		&.invoice {
			@include bg-image('invoice_2');
		}
		&.special {
			@include bg-image('special_2');
		}
	}

	.large {
		width: 12px;
		height: 12px;
		background-size: 12px 12px;
		&.decrease {
			@include bg-image('decrease_3');
		}
		&.discount {
			@include bg-image('discount_3');
		}
		&.guarantee {
			@include bg-image('guarantee_3');
		}
		&.invoice {
			@include bg-image('invoice_3');
		}
		&.special {
			@include bg-image('special_3');
		}
	}
</style>