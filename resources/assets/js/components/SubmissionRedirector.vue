<template>
	<section>
		<loading v-if="loading"></loading>
	</section>
</template>

<script>
	import Loading from '../components/Loading.vue'

    export default {
        components: {Loading},

        data: function () {
            return {
                loading: true
            }
        },

        created () {
            this.getSubmission()
        },

        methods: {
            getSubmission() {
				axios.get('/get-submission-by-id', {
				    params: {
				    	id: this.$route.params.id
				    }
				}).then((response) => {
					this.loading = false

				    this.$router.push('/c/' + response.data.category_name + '/' + response.data.slug)
				}).catch((error) => {
					this.loading = false;

					if (error.response.status === 404) {
						this.$router.push('/deleted-submission')
					}
				});
            }
        }
    };
</script>
