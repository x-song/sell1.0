<template>
   <div class="title">
        <div class="line"></div>
        <div class="text">{{name}}</div>
        <div class="line"></div>
    </div>
</template>

<script>



export default {
	props:{
		name:{
			type:String
		}
	}
	
}
</script>


<style lang="scss" scoped>
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
</style>