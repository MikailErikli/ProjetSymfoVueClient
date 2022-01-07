<template>
    <form @submit.prevent="onSubmit">
        <span class="help is-danger" v-text="errors"></span>

        <div class="field">
            <div class="control">
                <input class="input" type="title" placeholder="enter pin title..." v-model="title" @keydown="errors = ''">
            </div>
        </div>

         <div class="field">
            <div class="control">
                <input class="input" type="description" placeholder="enter pin Description..." v-model="description" @keydown="errors = ''">
            </div>
        </div>

         <button class="button is-primary">Add pin</button>
    </form>
</template>
<script>

import axios from 'axios'

export default {
    data() {
        return {
            title: '',
            description: '',
            errors: '',
        }
    },
    methods: {
        onSubmit() {
            this.postPin()
        },
        async postPin() {

    
            
            axios.post('http://localhost:8000/api/pins', this.$data)
                .then(response => {
                    this.title = ''
                    this.description = ''
                    this.$emit('completed', response.data)
                })
                .catch(error => {
                    // handle authentication and validation errors here
                    console.log("ERRR::", error.response.data);
                   
                })
        }
    }
}
</script>