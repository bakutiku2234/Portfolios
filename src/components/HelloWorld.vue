<template>
  <div class="hello">
    <myheader></myheader>
    <p v-if="msg.length > 0" >
      {{ msg }}
    </p>
    <p v-else>
      no text
    </p>
    <input type="text" v-model="msg" />
    <button @click="clear()">clear</button>
    <button @click="revert()">revert</button>
  </div>
</template>

<script>
import myheader from './myheader'

export default {
  name: 'HelloWorld',
  components: {
    myheader
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    clear () {
      this.msg = ''
    },
    revert () {
      this.msg = 'Welcome to Your Vue.js App'
    }
  },
  created () {
    var that = this
    $.getJSON('http://www.geonames.org/postalCodeLookupJSON?postalcode=10504&country=US&callback=?', {}, function (json) {
      console.log(json)
      that.msg = json.postalcodes[0].adminName1
    })
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
