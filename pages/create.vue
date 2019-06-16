<template>
    <article>
        <section>
            <h1>Holaluz price charts</h1>
            <div>
                <div class="chart"></div>
                <ul>
                    <li v-for="prices in prices" class="item">
                        <nuxt-link :to="'/prices/' + (data.unprecio)"</nuxt-link>
                    </li>
                </ul>
            </div>
        </section>
    </article>    
</template>
<script>
  import axios from 'axios'

  export default {
    async asyncData () {
      const {data} = await axios.get('http://localhost:3000/prices.json')
    //    console.log(data.unprecio);
      return {prices:data}
    }
  }
</script>
<style>

</style>