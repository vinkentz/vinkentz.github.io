<template lang="html">
  <div class="container">
    <br>
    <h5>Home>Lagu>DetailLagu</h5>
    <br>

    <h1 class="text-center">{{$route.params.id}}</h1>

    <br>

    <div class="text-center" v-for="(i, index) in detail_lagu" :key="index">
      <span v-if="i.labellirik">
        <p v-html="i.labellirik.value"></p>
      </span>
    </div>

    <br>
    
    <div class="text-center" v-for="(i, index) in detail_lagu" :key="index">
        <span v-if="i.source">
          <p class="text-justify"><strong>Source: </strong><br><a :href="i.source.value">{{i.source.value}}</a></p>
        </span>
    </div>

    <br>

    <table class="table">
      <thead>
        <th>Nada Dasar</th>
        <th>Birama</th>
        <th>Pengarang</th>
        <th>Provinsi</th>
      </thead>
      <tbody>
        <tr v-for="(i, index) in detail_lagu" :key="index">
          <td v-if="i.labelnadadasar">
            {{i.labelnadadasar.value}}
          </td>
          <td v-else>
            -
          </td>
          <td v-if="i.labelbirama">
            {{i.labelbirama.value}}
          </td>
          <td v-else>
            -
          </td>
          <td v-if="i.labelpengarang">
              <router-link to="/detailsPengarangLagu">
              <span v-if="i.pengarang">
                <a @click="detailsPengarangLagu(i.pengarang.value); dbpediaLink(i.linkpengarang.value)">{{i.labelpengarang.value}}</a>
               </span> 
              </router-link>
          </td>
          <td v-else>
            -
          </td>
          <td v-if="i.labelprovinsi">
            {{i.labelprovinsi.value}}
          </td>
          <td v-else>
            -
          </td>
        </tr>
      </tbody>
    </table>

    <br><br>

  </div>
</template>

<script>
import { mapState, mapActions } from "vuex"

export default {
  mounted() {
    this.$store.dispatch('detailLagu', this.$route.params.id)
    this.$store.dispatch('dbpediaLink')
  },
  computed: {
    ...mapState([
      'detail_lagu',
    ])
  },
  methods: {
    ...mapActions([
      'detailLagu',
      'dbpediaLink',
      'detailsPengarangLagu',
    ]),
  },
}
</script>

<style lang="css" scoped>
</style>
