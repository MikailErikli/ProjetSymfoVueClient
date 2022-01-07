<template>
<body>
  <center><h1>Premier Tests Api Platform</h1></center>

    <div class="container">
        <button class="button is-primary" @click="print()" >Add pin</button>
        <table class="table">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Title</th>
                    <th>description</th>
                    <th>image</th>
                </tr>
            </thead>
            <tbody>
                <template v-for="pin in pins">
                    <tr v-bind:key="pin.id">
                        <td>{{ pin.id }}</td>
                        <td>{{ pin.title }}</td>
                        <td>{{ pin.description }}</td>
                        <td>{{ pin.image_name }}</td>
                    </tr>
                </template>
            </tbody>
        </table>
     <pin-form @completed="addPins"></pin-form>
    </div>
</body>
</template>

<script>
import axios from 'axios'
import pinForm from './pinForm.vue'

export default {
     components: {
        pinForm
    },
    data() {
        return {
            pins: {}
        }
    },
    async created () {
      try {
            const response = await axios.get('http://127.0.0.1:8000/api/pins/liste')
            this.pins = response.data
           
        } catch(e) {
            // handle authentication error here
        }
    },
   


     methods: {
         addPins(pin) {
            this.pins.push(pin)
        },

        print(){
        console.log(this.pins);
    
        },
  
  },
}
</script>