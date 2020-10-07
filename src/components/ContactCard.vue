<template>
	<div class="contact-card">
		<div class="contact-photo">
			<img class="contact-photo-img" :src="profileAvatar"></img>
		</div>
		<div class="contact-info">
			<p class="contact-name">
				{{ firstName }} - {{ lastName }}
			</p>
			<p class="contact-gender">{{ gender }}</p>
			<p class="contact-email">{{ contactEmail }}</p>
		</div>
	</div>
</template>

<script>
export default {
	name: 'ContactCard',

	data () {
		return {

		}
	},

	props: {
		firstName: {
			type: String,
			required: true,
		},
		lastName: {
			type: String,
			required: true,
		},
		contactEmail: {
			type: String,
			required: true,
		},
		gender: {
			type: String,
			required: true,
		},
		profileAvatar: {
			type: String,
			required: true,
		}
	}
}
</script>

<style lang="scss" scoped>
	.contact {
		&-card {
			display: flex;
			margin-bottom: 12px;
			box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
			transition: all 0.3s cubic-bezier(.25,.8,.25,1);
		}
		&-photo {
			width: 100px;
			height: 100px;
			padding: 6px;

			&-img {
				width: 100%;
				height: 100%;
			}
		}
		&-info {
			flex: 1;
			padding: 4px 8px;

			p {
				margin-bottom: 6px;
			}
		}
	}


</style>