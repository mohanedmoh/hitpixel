<template>
  <div class="hello">
   <div>
    <b-form @submit="onSubmit" @reset="onReset">
      
      <b-form-group
        id="input-group-1"
        label="IP address :"
        label-for="input-1"
      >
        <b-form-input
          id="input-1"
          v-model="form.ip"
          type="text"
          placeholder="ip"
          required
        ></b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  
  </div>
  </div>
</template>

<script>
import axios from 'axios';

 export default {
    data() {
      return {
        responseV:null,
        form: {
          ip: '',
        }
      }
    },
    methods: {
      onSubmit(event) {
        event.preventDefault()
               axios.defaults.headers.common['Content-Type'] = null;
axios.defaults.headers.post['Accept'] = 'application/json'  // default header for all POST request

console.log(JSON.stringify(this.form));
axios.post("https://api.hitpixel.io/test/whitelist", JSON.stringify(this.form), {
            headers: {
            }
            })
            .then(function(response) {
alert(JSON.stringify(response.data));
                console.log(response);
            })
            .catch(function (error) {
                console.log(error);
            });
        },
    
        //alert(JSON.stringify(this.form))
     
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.form.ip = ''
       
       
      }
    }
  }
</script>