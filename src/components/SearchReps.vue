// PARENT
<template lang="html">
    <section class="search-reps">
        <v-row>
            <v-col cols="6">
                <v-card>
                    <v-card-text>
                        <v-subheader class="pa-0">
                            Where do you live?
                        </v-subheader>
                        <v-form ref="form">
                            <v-text-field
                                label="Postal Code"
                                required
                                v-on:keyup="CheckInputContent"
                                v-model="search"
                            ></v-text-field>
                        </v-form>
                        <v-btn v-on:click="CreateRepList()" clickclass="mr-4"
                            >Submit
                        </v-btn>
                    </v-card-text>
                </v-card>

                <div id="reprenstatives-list" v-show="hasContent">
                    <div>
                        <v-card
                            v-for="member in congressMembers"
                            :key="member.name"
                            v-on:click="repSelected()"
                        >
                            <v-card-title v-text="member.name"></v-card-title>
                            <v-card-subtitle
                                v-text="member.title"
                                style="text-align:left"
                            >
                            </v-card-subtitle>
                            <v-card-subtitle
                                v-text="member.city"
                                style="text-align:left"
                            >
                            </v-card-subtitle>
                        </v-card>
                    </div>
                </div>
            </v-col>
            <v-col cols="6"
                >//LETTER DISPLAY CHILD HERE<letter-display
                    :congressMembers="congressMembers"
                ></letter-display
            ></v-col>
        </v-row>
    </section>
</template>

<script lang="js">
import LetterDisplay from '@/components/LetterDisplay.vue';
import axios from 'axios';

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
          congressMembers:[],
	      hasContent: false,
          search: ""
      }
    },
    methods: {
        CheckInputContent: function () {
				if (this.search != "") {
					this.hasContent = true;
				} else {
					this.hasContent = false;
				}
			},
        async CreateRepList() {
        try {
            const res = await axios.get(
                'https://murmuring-headland-63935.herokuapp.com/api/amplify/' + this.search
            );
            this.congressMembers = res.data;
            this.hasContent=true;
            console.log(res.data);
        } catch (e) {
            console.error(e);
        }
    },
    repSelected(){
        console.log("clicked");
    }
}
}
</script>

<style scoped lang="less">
.search-reps {
}
</style>
