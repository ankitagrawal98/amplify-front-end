<template lang="html">
    <section class="search-reps">
        <v-row>
            <v-col cols="6">
                <v-card>
                    <v-card-text>
                        <v-subheader class="pa-0">
                            Where do you live?
                        </v-subheader>
                        <v-form ref="form" lazy-validation>
                            <v-text-field
                                :counter="10"
                                label="Postal Code"
                                required
                                v-on:keyup="CheckInputContent"
                            ></v-text-field>
                        </v-form>
                        <v-btn
                            v-model="search"
                            v-on:click="CreateRepList()"
                            clickclass="mr-4"
                            >Submit</v-btn
                        >
                    </v-card-text>
                </v-card>
            </v-col>
            <v-col cols="6"><letter-display></letter-display></v-col>
        </v-row>
    </section>
</template>

<script lang="js">
import LetterDisplay from '@/components/LetterDisplay.vue';

  export default  {
    name: 'SearchReps',
    components:{
        LetterDisplay
    },
    props: [],
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {
        CreateRepList: function () {
				this.congressMembers = [];
				this.$http
					.get(
						"https://murmuring-headland-63935.herokuapp.com/api/amplify/" +
							this.search
					)

			},

    },
    computed: {

    }
}
</script>

<style scoped lang="less">
.search-reps {
}
</style>
