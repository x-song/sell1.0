<template>
  <div class="food" v-show="showFlag" transition="move">
  	<div class="food-content">
  		<div class="image-header">
  			<img :src="food.image">
  			<div class="back" @click="hide()">
  				<i class="icon-arrow_lift"></i>
  			</div>
  			<div class="content">
  				<h1 class="title">{{food.name}}</h1>
  				<div class="detail">
  					<span class="select-count">月售{{food.sellCount}}</span>
  					<span class="rating">{{food.rating}}</span>
  				</div>
  				<div class="price">  					
  					<span class="now">￥{{food.price}}</span>
  					<span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
  				</div>
  			</div>
  		</div>

  	</div>
  </div>
</template>

<script>

export default {
  props:{
  	food:{
			type:Object
		}
  },
  data () {
    return {
      showFlag:false
    }
  },
  methods:{

  	show(){
  		this.showFlag = true;
  	},
  	hide(){
  		this.showFlag = false;
  	}
  }
}

</script>


<style lang="scss" scoped>
	.food{
		position: fixed;
		left:0;
		top: 0;
		bottom: 48px;
		z-index: 30;
		width: 100%;
		background-color: #fff;
		&.move-transition{
			transition:all 0.2s linear;
			transform:translate3d(0,0,0);
		}
		&.move-enter,&.move-leave{
			transition:all 0.2s linear;
			transform:translate3d(100%,0,0);
		}
		.image-header{
			position: relative;
			width: 100%;
			height: 0;
			padding-top: 100%;
			img{
				position: absolute;
				left: 0;
				top: 0;
				width: 100%;
				height: 100%;
			}
			.back{
				position: absolute;
				top: 10px;
				left: 0;
				.icon-arrow_lift{
					display: block;
					padding: 10px;
					font-size: 20px;
					color: #fff;
				}
			}	
		}
		.content{
			padding:18px;
			.title{
				line-height: 14px;
				margin-bottom: 8px;
				font-size: 14px;
				font-weight: 700;
				color: rgb(7,17,27);
			}
			.detail{
				margin-bottom: 18px;
				line-height: 10px;
				font-size: 0;
				height: 10px;
			}
			.sell-count,.rating{
				font-size: 10px;
				color: rgb(147,153,159);
			}
			.sell-count{

			}
		}

	}
</style>
