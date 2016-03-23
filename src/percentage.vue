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
				percentage: "",
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
				}
				return;
			},
			getPresent() {
				return Math.round(new Date().getTime() / 1000);
			},
			calcPercentage() {
				let result = (this.getPresent() - this.start) / (this.end - this.start) * 100;
				this.percentage = Math.round(result);
			}
		}
	}
</script>