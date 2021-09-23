<template>
    <v-container>
        <v-sheet v-if="zxcvbnResult" class="pl-3 pr-3">
            <v-row class="font-weight-bold">
                Security:
                <div class="font-weight-bold pl-1" :class="zxcvbnResult.color + '--text'">{{ zxcvbnResult.title }}</div>
                <v-progress-linear :color="zxcvbnResult.color" :value="zxcvbnResult.width"></v-progress-linear>
            </v-row>
        </v-sheet>
    </v-container>
</template>

<script>
var zxcvbn = require('zxcvbn');

export default {
    data() {
        return {
            score: 0,
            stats: [
                {
                    title: 'Very Weak',
                    width: 20,
                    color: 'red',
                },
                {
                    title: 'Weak',
                    width: 40,
                    color: 'red',
                },
                {
                    title: 'Good',
                    width: 60,
                    color: 'orange',
                },
                {
                    title: 'Strong',
                    width: 80,
                    color: 'green',
                },
                {
                    title: 'Very Strong',
                    width: 100,
                    color: 'green',
                },
            ],
        }
    },
    computed: {
        zxcvbnResult: function () {
            if (!this.input) return false
            var zxcvbnObj = zxcvbn(this.input)
            this.$emit('update:score', zxcvbnObj.score)
            return this.stats[zxcvbnObj.score]
        },
    },
    props: {
        input: {
            type: String,
            required: true,
        },
    },
}
</script>
