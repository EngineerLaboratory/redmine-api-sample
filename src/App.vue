<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <b-card bg-variant="light">
      <b-form-group
        label-cols-lg="3"
        label="Redmine infomasion"
        label-size="lg"
        label-class="font-weight-bold pt-0"
        class="mb-0"
      >
        <!-- URL -->
        <b-form-group
          label="URL:"
          label-for="nested-url"
          label-cols-sm="3"
          label-align-sm="right"
        >
          <b-form-input 
            id="nested-url"
            type="url"
            v-model="url"
          ></b-form-input>
        </b-form-group>

        <!-- Query ID -->
        <!-- <b-form-group
          label="Query ID:"
          label-for="nested-query"
          label-cols-sm="3"
          label-align-sm="right"
        >
          <b-form-input
            id="nested-query"
            type="number"
            v-model="query"
          ></b-form-input>
        </b-form-group> -->

        <!-- Access Key -->
        <b-form-group
          label="Access Key:"
          label-for="nested-access"
          label-cols-sm="3"
          label-align-sm="right"
        >
          <b-form-input
            id="nested-access"
            type="text"
            v-model="accessKey"
          ></b-form-input>
        </b-form-group>

        <!-- Button -->
        <b-form-group
          label-for="nested-access"
          label-cols-sm="11"
          label-align-sm="right"
        >
          <b-button variant="primary" @click="action">Primary</b-button>
        </b-form-group>
      </b-form-group>
      <b-form-textarea
       v-model="jsontext"
       placeholder="Enter something..."
       rows="3"
       max-rows="6"
       >
      </b-form-textarea>
    </b-card>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  components: {
    // HelloWorld
  },
  data() {
    // 
    return {
      url: "https://localhost/custom_fields.json"
      // , project: ""
      // , query: 8
      , accessKey: ""
      , jsontext: ""
    }
  },
  methods: {
    // 
    action() {
      // 
      console.log( "### Below ###" )
      console.log(this.url)
      // console.log(this.project)
      // console.log(this.query)
      console.log(this.accessKey)

      // 
      axios.defaults.headers.common['Access-Control-Allow-Origin'] = '*';
      axios.defaults.headers.common['Content-Type'] = 'application/json';
      axios.defaults.headers.common['X-Redmine-API-Key'] = this.accessKey;
      axios.defaults.headers.common['Access-Control-Allow-Methods'] = 'GET, POST, DELETE, PUT, OPTIONS, HEAD';
      axios.defaults.headers.common['Access-Control-Max-Age'] = 0;
      axios.defaults.headers.common['Access-Control-Allow-Credentials'] = true;
      axios.defaults.headers.common['X-Rack-CORS'] = 'hit';
      // axios.defaults.withCredentials = true;

      // let instance = axios.create({
      //   baseURL: "http://localhost:3000"
      //   , responseType: 'json'
      // })
      
      axios.get(this.url
      , {
        // params: { query_id: this.query }
      })
      .then(function (response) {
      // handle success(axiosの処理が成功した場合に処理させたいことを記述)
        console.log(response);
        this.jsontext = response.data;
      })
      .catch(function (error) {
        console.log(error);
      })
      .finally(function () {});
      console.log( "### Abobe ###" );
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
