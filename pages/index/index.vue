<template>
	<view class="content">
		<view class="ligth" :style="{transform: 'translate('+item.x+'px,'+-item.y+'px) scale('+item.y/200+1+','+item.y/200+1+')',background:'rgba('+item.rgba+')',boxShadow: '0px 0px 10px 5px rgba('+item.rgba+')',width:item.size+'px',height:item.size+'px',opacity:300/item.y+0.3}"
		 v-for="(item,index) in ligth" :key="index"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				ligth: []
			}
		},
		onLoad() {
			//随机光点
			const {
				windowWidth,
				windowHeight
			} = uni.getSystemInfoSync();
			
			setInterval(() => {
				let x = Math.random() * windowWidth
				let y = Math.random() * 120
				let size = Math.random() * 10 + 6
				let rgba = ""
				for(let i=0,len=3;i<len;i++){
					rgba += Math.random()*255+","
				}
				rgba += Math.random()*0.8
				this.ligth.push({
					x,
					y,
					size,
					rgba
				})
			},500)
			
			setInterval(() => {
				for(let i=0,len=this.ligth.length;i<len;i++){
					this.ligth[i].y += (this.ligth[i].y/200+1)
					if(this.ligth[i].y > windowHeight){
						this.ligth.splice(i,1)
						len --
						i--
					}
				}
			},30)

		},
		methods: {

		}
	}
</script>

<style>
	.content {
		position: fixed;
		width: 100%;
		height: 100%;
		background: linear-gradient(30deg, #290043, #050018);
	}

	.ligth{
		position: fixed;
		bottom:0px;
		border-radius: 50%;
	}
</style>
