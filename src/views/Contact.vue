<template>
	<div class="contact">
		<div class="contact-title">
			Contact
		</div>
		<div class="text-center contact-loading" v-if="isLoading">
			<b-spinner label="Spinning"></b-spinner>
		</div>
		<template v-else>
			<div class="contact-wrapper" >
				<contact-card
					v-for="
						contactItem, index 
						in slicedContactData" 
					:profile-avatar="contactItem.avatar"
					:first-name="contactItem.first_name"
					:last-name="contactItem.last_name"
					:contact-email="contactItem.email"
					:gender="contactItem.gender"
					:key="index"
				></contact-card>
			</div>
			<div class="contact-paging">
				<b-button 
					class="contact-button-prev" 
					@click="prevPage()" 
					:disabled="pagination.currentPage == 0"
				>
					Previous
				</b-button>
				<b-button 
					class="contact-button-next" 
					@click="nextPage()"
					:disabled="slicedContactData.length < pagination.count"
				>
					Next
				</b-button>
			</div>
		</template>

	</div>
</template>

<script>
import ContactCard from '@/components/ContactCard.vue';
import axios from 'axios';

export default {
	name: 'Contact',

	components: {
		ContactCard
	},

	computed: {
		_token () {
			return localStorage.getItem('tonjoo_token');
		},

		slicedContactData() {
			return this.contactData.slice(
				this.pagination.currentIndex, 
				this.pagination.currentIndex + this.pagination.count)
		}
	},

	data () {
		return {
			isLoading: false,
			contactData: [],

			// makeshift pagination
			pagination: {
				count: 5,
				currentPage: 0,
				currentIndex: 0,
			}
		}
	},

	mounted() {
		if(this._token) {
			this.generateContact();
		} else {
			this.$router.push('/');
		}
	},

	methods: {
		generateContact () {
			this.isLoading = true;
			axios
				.get(`https://private-anon-d914e434db-tonjoorecruitment.apiary-mock.com/recruitment-api/contacts?token=${this._token}`)
				.then(response => {
					// this.contactData = response.data.data;
					this.isLoading = false

					// for the sake of duplication simulation, 
					// on the real code I would never do this I promise
					for (let i = 0; i < 8; i++) {
						this.contactData.push(response.data.data[0]);
					} 
				});
		},


		nextPage() {
			this.pagination.currentPage += 1;
			this.pagination.currentIndex = this.pagination.count * this.pagination.currentPage

		},
		prevPage() {
			this.pagination.currentPage -= 1;
			this.pagination.currentIndex = this.pagination.count * this.pagination.currentPage

		}
	},

}
</script>


<style scoped="">
	.contact {
		height: 100vh;
		display: flex;
		flex-direction: column;
	}
	.contact-title {
		background-color: #333;
		color: #fafafa;
		text-align: center;
		padding: 12px 0;
		font-size: 24px;
	}

	.contact-loading {
		margin-top: 30px;
	}

	.contact-wrapper {
		padding: 12px;
		height: 100%;
		overflow: scroll;
	}

	.contact-paging	{
		display: flex;
		justify-content: space-between;
		padding: 12px;
	}

	.contact-button-next, .contact-button-prev {
		width: 90px;
	}

</style>