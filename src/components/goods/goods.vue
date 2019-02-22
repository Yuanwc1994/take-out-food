<template>
	<div class="goods">
		<div class="menu-wrapper">
			<ul>
				<li v-for="item in goods" class="menu-item">
					<span class="text border-1px">
						<icon v-show="item.type > 0" size="large" :type="item.type"></icon>{{item.name}}
					</span>
				</li>
			</ul>
		</div>
		<div class="foods-wrapper">
			<ul>
				<li v-for="item in goods" class="food-list">
					<h1 class="title">{{item.name}}</h1>
					<ul>
						<li v-for="food in item.foods" class="food-item border-1px">
							<div class="icon">
								<img :src="food.icon" width="57" height="57">
							</div>
							<div class="content">
								<h2 class="name">{{food.name}}</h2>
								<p class="desc">{{food.description}}</p>
								<div class="extra">
									<span class="count">月售{{food.sellCount}}份</span>
									<span>好评率{{food.rating}}%</span>
								</div>
								<div class="price">
									<span class="now">&yen;<i>{{food.price}}</i></span>
									<span class="old" v-show="food.oldPrice">&yen;<i>{{food.oldPrice}}</i></span>
								</div>
							</div>
						</li>
					</ul>
				</li>
			</ul>
		</div>
	</div>
</template>

<script type="text/ecmascript-6">
	import icon from 'components/icon/icon';

	const ERR_OK = 0;

	export default {
		props: {
			seller: {
				type: Object
			}
		},
		data() {
			return {
				goods: []
			};
		},
		created() {
			this.$http.get('/api/goods').then((response) => {
				response = response.body;
				if (response.errno === ERR_OK) {
					this.goods = response.data;
					// console.log(this.goods);
				}
			});
		},
		components: {
			icon
		}
	};
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
	@import "../../common/styles/mixin.scss";

	$color: rgb(147, 153, 159);

	.goods {
		display: flex;
		position: absolute;
		top: 174px;
		bottom: 46px;
		width: 100%;
		overflow: hidden;
		.menu-wrapper {
			flex: 0 0 80px;
			width: 80px;
			background-color: #f3f5f7;
			.menu-item {
				display: table;
				width: 56px;
				height: 54px;
				line-height: 14px;
				padding: 0 12px;
				.icon {
					margin-right: 2px;
				}
				.text {
					display: table-cell;
					width: 56px;
					vertical-align: middle;
					@include border-1px(rgba(7, 17, 27, 0.1));
					font-size: 12px;
				}
			}
		}
		.foods-wrapper {
			flex: 1;
			.title {
				padding-left: 14px;
				height: 26px;
				line-height: 26px;
				border-left: 2px solid #d9dde1;
				font-size: 12px;
				color: $color;
				background-color: #f3f5f7;
			}
			.food-item {
				display: flex;
				margin: 18px;
				padding-bottom: 18px;
				@include border-1px(rgba(7, 17, 27, 0.1));
				&:last-child{
					@include border-none();
					margin-bottom: 0;
				}
				.icon {
					flex: 0 0 57px;
					margin-right: 10px;
				}
				.content {
					flex: 1;
					.name {
						margin: 2px 0 8px;
						height: 14px;
						line-height: 14px;
						font-size: 14px;
						color: rgb(7, 17, 27);
					}
					.desc,.extra{
						font-size: 10px;
						line-height: 10px;
						color: $color;
					}
					.desc {
						margin-bottom: 8px;
					}
					.extra {
						.count {
							margin-right: 12px;
						}
					}
					.price {
						line-height: 24px;
						font-size: 10px;
						.now {
							margin-right: 8px;
							color: rgb(240, 20, 20);
							i {
								font-size: 14px;
								font-weight: 700;
							}
						}
						.old {
							text-decoration: line-through;
							color: $color;
							i {
								font-weight: 700;
							}
						}
					}
				}
			}
		}
	}
</style>