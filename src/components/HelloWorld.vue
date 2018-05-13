<template>
  <div >
      <input type="text" v-model="input">
      <button @click="calcResult">result</button>
      <div v-html="showResult">
      </div>
  </div>
</template>

<script>
import * as _ from 'lodash'
export default {
  name: 'HelloWorld',
  data () {
    return {
      input : "",
      showResult : ""
    }
  },
  methods: {
    handleNumber(number){ 
      if(!_.toString(number).match(/^\d+$/)) return ""
      const result =  _.toArray(_.toString(number)).reduce((a,b) => {
          return +a + +b
      })
      this.showResult += `-> ${_.toArray(_.toString(number)).join("+")}`
      this.showResult += `<br>`
      this.showResult += `-> ${_.toString(result)}`
      this.showResult += `<br>`
      return _.toString(result)
    },
    loadNumber(number){
      let result = number
      do{
          result = this.handleNumber(result)
      }
      while (result.length > 1)
    },
    calcResult () {
      this.showResult = ""
      this.loadNumber (this.input)
    }
  }
}
</script>

