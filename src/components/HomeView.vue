<template>
   <div class="container">
         <div class="card">
      <div class="card-header text-center">
            <div>
                <input type="file" id='file' ref="file" />
                <button v-on:click="uploadFile()">Upload!</button>
            </div>
      </div>
      <div class="card-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">First Name</th>
              <th scope="col">Last Name</th>
              <th scope="col">Date of Birth</th>
              <th scope="col">DS Division</th>
              <th scope="col">Actions</th>
            </tr>
          </thead>
          <tbody>

          </tbody>
        </table>
      </div>

    </div>
    </div>
</template>

<script>
import axios from 'axios';

  export default {

    name: 'HomeView',

    data() {
        return {
                file:'',
            }
        },

        methods: {
            uploadFile: function () {
                this.file = this.$refs.file.files[0];
                let formData = new FormData();
                formData.append('file', this.file);
                this.$refs.file.value = '';
                axios.post('http://127.0.0.1:8000/api/post-file', formData, {
                    headers: {
                        'Content-Type': 'multipart/form-data'
                    }
                })
                .then(function (response) {
                    console.log(response);
                })
                .catch(function (error) {
                    console.log(error);
                });                
            }          
        },
    }
</script>
