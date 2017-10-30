<template>
  <div class="header">
      <div class="content-wraper">
      	<div class="avatar">
      		<img :src="seller.avatar" width="64" height="64">
      	</div>
      	<div class="content">
      		<div class="title">
      			<span class="brand"></span>
      			<span class="name">{{seller.name}}</span>
      		</div>
      		<div class="description">
      			{{seller.description}}/{{seller.deliveryTime}}分钟送达
      		</div>
      		<div class="support" v-if="seller.supports">
      			<span class="icon" :class="classMap[seller.supports[0].type]"></span>
      			<span class="text">{{seller.supports[0].description}}</span>
      		</div>
      	</div>
        <div v-if="seller.supports" @click="showDetail" class="support-count">
            <span class="count">{{seller.supports.length}}个</span>
            <i class="icon-keyboard_arrow_right"></i>
        </div>
      </div>
    <div class="bulletin-wraper">
        <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
         <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
          <img :src="seller.avatar" width="100%" height="100%" alt="">
    </div>
    <div class="detail" v-show="detailShow" transition="fade">
        <div class="detail-wrapper clearfix">
            <div class="detail-main">
              <h1 class="name">{{seller.name}}</h1>
              <div class="star-wrapper">
                <star :size="48" :score="seller.score"></star>
                <title name="优惠信息"></title>

                <ul v-if="seller.supports" class="supports">
                  <li class="support-item" v-for="item in seller.supports">
                    <span class="icon" :class="classMap[seller.supports[$index].type]"></span>
                    <span class="text">{{seller.supports[$index].description}}</span>
                  </li>
                </ul>
                <title name="商家公告"></title>
                <div class="bulletin">
                    <p class="content">{{seller.bulletin}}</p>
                  
                </div>
              </div>
            </div>
        </div>
        <div class="detail-close">
            <i class="icon-close"  @click="showClose"></i>
        </div>
    </div>
  </div>
</template>

<script>

import star from 'components/star/star'
import title from 'components/title/title'

export default {
	props: {
		seller:{
			type:Object
		}
	},
  data(){
    return{
      detailShow:false
    }
  },
  methods:{
    showDetail(){
      this.detailShow=true; 
    },
    showClose(){
       this.detailShow=false; 
    }
  },
  created(){
    this.classMap = ['decrease','discount','guarantee','invoice','special'];
  },
  components:{
    star,
    title
  }

}
</script>


<style lang="scss" scoped>
  @import '../../common/sass/icon.scss';
  @import '../../common/sass/mixin.scss';

    .header{
      color:#fff;
      position: relative;
      overflow:hidden;
      background:rgba(7,17,27,0.5);
      .content-wraper{
        padding:24px 12px 18px 24px;
        font-size:0;
        position: relative;
        .avatar{
            display:inline-block;
            img{
              border-radius:2px;
            } 
        }
        .content{
            display:inline-block;
            font-size:14px;
            margin-left:16px;
            .title{
               margin:2px 0 8px 0;
               width: 100%;
               .brand{
                  vertical-align:top;
                  width: 36px;
                  height: 18px;
                  display: inline-block;
                  @include bg_img('brand');
                  background-size:30px 18px;
                  background-repeat:no-repeat;
                }
                .name{
                    margin-left:6px;
                    font-size:16px;
                    line-height:18px;
                    font-weight:bold;
                  }
               
             }
             .description{
              margin-bottom:10px;
              line-height:12px;
              font-size:12px;
            }
             .support{
                .icon{
                  vertical-align:top;
                  display:inline-block;
                  width:12px;
                  height:12px;
                  margin-right:4px;
                  background-size:12px 12px;
                  background-repeat:no-repeat;
                    &.discount{
                       @include bg_img('discount_1');
                    }
                    &.decrease{
                       @include bg_img('decrease_1');
                    }
                    &.guarantee{
                       @include bg_img('guarantee_1');
                    }
                    &.invoice{
                       @include bg_img('invoice_1');
                    }
                    &.special{
                       @include bg_img('special_1');
                    }
                }
                 .text{
                  vertical-align:top;
                  line-height:12px;
                  font-size:12px;
                }
              } 
          }
        .support-count{
          position: absolute;
          right:12px;
          bottom:18px;
          padding:0 8px;
          height:24px;
          line-height:24px;
          border-radius:14px;
          background:rgba(0,0,0,0.2);
          text-align:center;
          .count{
            font-size:10px;
            vertical-align:top;
          }
          .icon-keyboard_arrow_right{
            font-size:10px;
            line-height:24px;
            margin-left:2px;
            display:inline-block;
          }
        }

      }
    .bulletin-wraper{
      position: relative;
      height:28px;
      line-height:28px;
      padding:0 22px 0 12px;
      white-space:nowrap;
      overflow:hidden;
      text-overflow:ellipsis;
      background:rgba(7,17,27,0.2);
      .bulletin-title{
        vertical-align:top;
        display:inline-block;
        margin-top:8px;
        width:22px;
        height:12px;
        @include bg_img('bulletin');
        background-repeat:no-repeat;
        background-size:22px 12px;
      }
      .bulletin-text{
        vertical-align:top;
        font-size:10px;
        margin:0 4px;
      }
      .icon-keyboard_arrow_right{
        position:absolute;
        font-size:10px;
        top:10px;
        right:8px;

      }
    }
    .background{
        position: absolute;
        top: 0;
        left:0;
        width:100%;
        height:100%;
        z-index:-1;
        filter:blur(10px);
    }
    .detail{
      position:fixed;
      width:100%;
      height:100%;
      left:0;
      top: 0;
      z-index:100;
      transition: all 0.5s;
      backdrop-filter:blur(10px);
      &.fade-transition{
        opacity:1;
        background:rgba(7,17,27,0.8);
      }
       &.fade-enter,&.fade-leave{
        opacity:0;
        background:rgba(7,17,27,0);
      }
      .detail-wrapper{
        min-height:100%;
        width: 100%;
        .detail-main{
          margin-top:64px;
          padding-bottom:64px;
          .name{
            line-height:16px;
            text-align:center;
            font-size:16px;
            font-weight:700;
          }
          .star-wrapper{
                margin-top:18px;
                padding:2px 0;
                text-align:center;    
              .title{
                display: flex;
                width:80%;
                margin:30px auto 24px auto;
                .line{
                  flex:1;
                  position:relative;
                  top:-6px;
                  border-bottom:1px solid rgba(255,255,255,0.2);
                }
                .text{
                  padding:0 12px;
                  font-size:14px;
                  font-weight:700;

                }
              }
              .supports{
                width: 80%;
                margin:0 auto;
                .support-item{
                  padding:0 12px;
                  margin-bottom:12px;
                  font-size:0;
                  text-align:left;
                  &:last-child{
                    margin-bottom:0;
                  }
                  .icon{
                    display: inline-block;
                    width:16px;
                    height:16px;
                    vertical-align:top;
                    margin-right:6px;
                    background-size:16px 16px;
                    background-repeat:no-repeat;
                    &.discount{
                       @include bg_img('discount_2');
                    }
                    &.decrease{
                       @include bg_img('decrease_2');
                    }
                    &.guarantee{
                       @include bg_img('guarantee_2');
                    }
                    &.invoice{
                       @include bg_img('invoice_2');
                    }
                    &.special{
                       @include bg_img('special_2');
                    }
                  }
                  .text{
                    line-height:16px;
                    font-size:12px;
                  }
                }
              }
              .bulletin{
                width: 80%;
                margin:0 auto;
                .content{
                  padding:0 12px;
                  line-height:24px;
                  font-size:12px;
                }
              }
          }

         }
      }
      .detail-close{
            position:relative;
            width: 32px;
            height:32px;
            margin:-64px auto 0 auto;
            clear:both;
            font-size:32px;
      }

    }
    }
    	
          
              
      				
      					
              
            
          
</style>  
