<template>
  <q-page class="flex flex-center">
    <q-editor v-model="editor" min-height="20rem" style="width: 100%" /> <br>
    <q-btn color="primary" label="SEND" style="width: 100%" @click="sendData()"/> <br>
    <q-btn color="secondary" label="READ" style="width: 100%" @click="readData()"/> <br>
    
      <div class="q-pa-md" style="width: 100%">
        <q-list bordered separator v-for="(item,i) in ayat" :key="i">
          <q-item clickable v-ripple>
            <q-item-section v-html="item.ayat"/>
          </q-item>
        </q-list>
      </div>
  </q-page>
</template>

<style>
</style>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      editor: '',
      ayat:[]
    }
  },
  methods: {
  sendData () {
    this.$axios.get('http://maisarahpauzi.com/newdata.php?text='+this.editor)
      .then((response) => {
        console.log('success')
      })
      .catch(() => {
        console.log('failed')
      })
  },
   readData () {
    this.$axios.get('http://maisarahpauzi.com/read_data.php')
      .then((response) => {
        this.ayat = response.data;
        console.log(response.data);
      })
      .catch(() => {
        console.log('failed')
      })
  }
}
}
</script>
