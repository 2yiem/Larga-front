<template>
  <form class="ml-8 text-center">
    <div class="input-control">
      <v-col cols="12" sm="12" md="4" lg="4" class="pd-0"><label>Chapter Registration</label></v-col>
      <v-col cols="12" md="4" lg="4" sm="12" class="pd-0">
        <v-text-field
          label="Chapter Name"
          placeholder="Chapter Name"
          v-model="title"
          dense
          outlined
        ></v-text-field>
      </v-col>
      <v-col cols="12" md="4" lg="4" sm="12" class="pd-0">
        <v-btn
          style="width: 100%"
          class="mt-1 mb-4 primary"
          @click="chapterRegistration"
        >Register Chapter</v-btn>
      </v-col>
    </div>
  </form>
</template>

<script>
export default {
  name: "index",
  data() {
    return {
      title: ''
    }
  },
  methods: {
    chapterRegistration() {
      const titles = {
        title: this.title
      }
      if (this.title !== "") {
        return this.$axios.post('chapter', titles).then((res) => {
          console.log(res.data)
          this.title = ''
        })
      }
    }
  }
}
</script>

<style scoped>
.input-control {
  margin-top: 100px;
}
</style>
