<template>
	<div class="home">
		<!-- <img alt="Vue log12o" src="../assets/logo.png"> -->
		<div class="login-wrapper">
			<p class="login-title">Tonjoo Test</p>

			 <b-form @submit.prevent="onSubmit" class="form-login">
				<b-form-group
					id="input-group-username"
					label="Username:"
					label-for="input-username"
				>
					<b-form-input
						id="input-username"
						v-model="username"
						type="text"
						required
						placeholder="Enter username"
					></b-form-input>
				</b-form-group>

				<b-form-group
					id="input-group-password"
					label="Password:"
					label-for="input-password"
				>
					<b-form-input
						id="input-password"
						v-model="password"
						type="password"
						required
						placeholder="Enter password"
					></b-form-input>
				</b-form-group>
				<b-button type="submit" class="input-button-login">
					<b-spinner label="Spinning" v-if="isLoading"></b-spinner>
					<template v-else>Login</template>
				</b-button>
			 </b-form>
		</div>
	</div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios';

export default {
	name: 'Home',

	data () {
		return {
			username: '',
			password: '',
			info: {},
			isLoading: false,
		};
	},

	// mounted() {

	// },

	methods: {
		onSubmit () {
			this.isLoading = true;

			const params = new URLSearchParams();
			params.append('username', this.username);
			params.append('password', this.password);

			const config = {
				headers: {
					'Access-Control-Allow-Origin': '*',
					'Access-Control-Allow-Headers': '*'
				}
			}

			axios
				.post('https://private-anon-9ee5accb21-tonjoorecruitment.apiary-mock.com/recruitment-api/authenticate', params)
				.then(response => {
					if(response.data) {
						this.isLoading = false;
						localStorage.setItem('tonjoo_token', response.data.token);
						this.$router.push('contact');
					}
				});
		}
	}
}
</script>

<style lang="scss" scoped>

	.home {
		padding: 30px 12px;
	}

	.login-wrapper {

	}

	.login-title {
		text-align: center;
		font-size: 24px;
	}

	.form-login {
		margin-top: 150px;
	}

	.input-button-login {
		display: block;
		margin: 100px auto 0;
		width: 80px;
	}
</style>