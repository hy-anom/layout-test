<template>
	<div id="app">
		<!-- <div id="nav">
			<router-link to="/">Home</router-link> |
			<router-link to="/contact">Contact</router-link>
		</div> -->
		<router-view/>
	</div>
</template>

<script>
export default {
	created() {
		if (this.$workbox) {
			this.$workbox.addEventListener("waiting", () => {
				this.showUpdateUI = true;
			});
		}
	},

	async accept() {
		this.showUpdateUI = false;
		await this.$workbox.messageSW({ type: "SKIP_WAITING" });
	}
}
</script>

<style lang="scss">
// wrapper
#app {
	max-width: 480px;
	width: 100%;
	margin: auto;
	height: 100vh;
	background-color: #fafafa;
}

#nav {
	padding: 30px;

	a {
		font-weight: bold;
		color: #2c3e50;

		&.router-link-exact-active {
			color: #42b983;
		}
	}
}
</style>
