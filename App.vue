<template>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import axios from 'axios';

@Component({
  components: {
  },
})
export default class App extends Vue {
  mounted(){
    this.get100thPrimeNumber();
  }
  private get100thPrimeNumber(): number{
    let count = 0;
    for(let i = 2;;i++){
      if(this.isNatural(i)) count++;
      if(count ==100) return i;
    }
    return -1;
  }
  private isNatural(number: number): boolean {
    for (var i = 2; i <= number/2; i++) {
        if (number % i == 0) {
            return false;
        }
    }
    return true;
  }
  private async getUrl(): Promise<void>{
    try{
      if(localStorage.getItem('url') == null){
        let url = await axios.get('http://localhost:5428/api/getUrl');
        localStorage.setItem('url', JSON.stringify(url.data));
      }
    }
    catch(error){
      console.log(error)
    }
  }
  private async setUrl(url: string): Promise<void>{
    try{
      await axios.post('http://localhost:5428/api/setUrl',url);
      localStorage.setItem('url', JSON.stringify(url));
    }
    catch(error){
      console.log(error)
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
