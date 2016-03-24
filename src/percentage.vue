<style scoped>

</style>
<template>
	<div>
		{{ percentage }}%
	</div>
</template>
<script> 
	export default {
		props: ["start","end"],
		data(){
			return {
				percentage: 0,
				timeoutTime: 10
			}
		},
		created(){
			this.timeoutTime = ((this.end - this.start) / 100) * 1000;
			this.loop();
		},
		methods: {
			loop() {
				let __self = this;
				
				if (this.end > this.getPresent()) {
					this.calcPercentage();
					setTimeout(function() {
						__self.loop();
					}, this.timeoutTime);
					return;
				}
				this.percentage = 100;
				return;
			},
			getPresent() {
				return new Date().getTime() / 1000;
			},
			calcPercentage() {
				let result = Math.round((this.getPresent() - this.start) / (this.end - this.start) * 100);
				
				if (result > 0) {
					this.percentage = result;
				}
			}
		}
	}
</script>