 <template>
  <div class="search">
  <h1>Curiosity</h1>
  <h2>Enter sol day, 0 - 2031</h2>
    <form v-on:submit.prevent="getResult(query)">
      <input type="text" placeholder="Front Hazard Avoidance Cam" v-model="query" />
    </form>
    <div v-if="results">

      <div v-for="result in results">

        <img v-bind:src="result.img_src">{{result.img_src}} />
        <p></p>
        <span>{{result.earth_date}}</span>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'search',
  data () {
    return {
      msg: 'Search',
      query: '',
      results: ''
    }
  },
  methods: {
    getResult(query) {
      axios.get('https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=' + query + '&camera=fhaz&media_type=image&api_key=DEMO_KEY').then( response => { 
      this.results = response.data.photos;
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
