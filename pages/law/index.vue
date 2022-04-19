<template>
  <v-app>
    <v-row>
      <v-col cols="12">
        <v-card>
          <v-toolbar
            flat
            color="primary"
            dark
            glow
          >
            <v-toolbar-title>LARGA DATA ENTRY</v-toolbar-title>
          </v-toolbar>
          <v-tabs
            background-color="transparent"
            color="basil"
            grow>
            <v-tab>
              Kinyarwanda LAW
            </v-tab>
            <v-tab>
              English LAW
            </v-tab>
            <v-tab>
              French LAW
            </v-tab>
            <v-tab-item>
              <v-card flat>
                <v-card-text>
                  <form class="ml-8 text-center">
                    <div class="input-control">
                      <v-row>
                        <v-col cols="12" sm="2" md="2" lg="2" class="pd-0">
                          <p>Kwandika Amategeko</p>
                          <v-select
                            :items="articles"
                            v-model="articleSelected"
                            label="Hitamo ingingo"
                            @change="retrieveArticleRW"
                            outlined
                          ></v-select>
                          <v-text-field
                            label="Article Name"
                            placeholder="Ingingo"
                            v-model="title"
                            dense
                            outlined
                          ></v-text-field>
                          <v-btn
                            style="width: 100%"
                            class="mt-1 mb-4 primary"
                            @click="lawRegistrationRW"
                          >Injiza ingingo</v-btn>
                        </v-col>
                        <v-col cols="12" sm="10" md="10" lg="10" class="pd-0">
                          <v-data-table
                            :items="laws"
                            :headers="headerLaws">
                          </v-data-table>
                        </v-col>
                      </v-row>
                    </div>
                  </form>
                </v-card-text>
              </v-card>
            </v-tab-item>
            <v-tab-item>
              <v-card flat>
                <v-card-text>
                  <form class="ml-8 text-center">
                    <div class="input-control">
                      <v-row>
                        <v-col cols="12" sm="2" md="2" lg="2" class="pd-0">
                          <p>Laws Registration</p>
                          <v-select
                            :items="articles_en"
                            v-model="articleSelected"
                            label="Choose Article"
                            @change="retrieveArticleEN"
                            outlined
                          ></v-select>
                          <v-text-field
                            label="Chapter Name"
                            placeholder="Article Name"
                            v-model="title"
                            dense
                            outlined
                          ></v-text-field>
                          <v-btn
                            style="width: 100%"
                            class="mt-1 mb-4 secondary"
                            @click="lawRegistrationEN"
                          >Register Article</v-btn>
                        </v-col>
                        <v-col cols="12" sm="10" md="10" lg="10" class="pd-0">
                          <v-data-table
                            :items="laws_en"
                            :headers="headerLaws">
                          </v-data-table>
                        </v-col>
                      </v-row>
                    </div>
                  </form>
                </v-card-text>
              </v-card>
            </v-tab-item>
            <v-tab-item>
              <v-card flat>
                <v-card-text>
                  <form class="ml-8 text-center">
                    <div class="input-control">
                      <v-row>
                        <v-col cols="12" sm="2" md="2" lg="2" class="pd-0">
                          <p>Registration de Loi</p>
                          <v-select
                            :items="articles_fr"
                            v-model="articleSelected"
                            label="Article"
                            @change="retrieveArticleFR"
                            outlined
                          ></v-select>
                          <v-text-field
                            label="Chapter Name"
                            placeholder="Chapter Name"
                            v-model="title"
                            dense
                            outlined
                          ></v-text-field>
                          <v-btn
                            style="width: 100%"
                            class="mt-1 mb-4 green"
                            @click="lawRegistrationFR"
                          > Registration Loi </v-btn>
                        </v-col>
                        <v-col cols="12" sm="10" md="10" lg="10" class="pd-0">
                          <v-data-table
                            :items="laws_fr"
                            :headers="headerLaws">
                          </v-data-table>
                        </v-col>
                      </v-row>
                    </div>
                  </form>
                </v-card-text>
              </v-card>
            </v-tab-item>
          </v-tabs>
        </v-card>
      </v-col>
    </v-row>
  </v-app>
</template>

<script>
export default {
  name: "index",
  mounted() {
    this.retrieveArticleEN()
    this.retrieveArticleFR()
    this.retrieveArticleRW()
    this.lawsRetrieve()
    this.lawsRetrieveEN()
    this.lawsRetrieveFR()
  },
  data: () => ({
    articles: [],
    articles_en: [],
    articles_fr: [],
    headerLaws: [
      { text: "#", value:"value"},
      { text: "Laws", value: "text"},
      { text: "Article", value: "article"},
      { text: "Chapter", value: "chapter"},
      { text: "Category", value: "category"}
    ],
    laws: [],
    laws_en: [],
    laws_fr: [],
    articleSelected: '',
    lawSelected: '',
    title: '',
  }),
  methods: {
    retrieveArticleRW() {
      return this.$axios.get('articlesRetrieveRW').then((res) => {
        this.articles = res.data
      })
    },
    retrieveArticleFR() {
      return this.$axios.get('articlesRetrieveFR').then((res) => {
        this.articles_fr = res.data
        console.log(this.articles_fr)
      })
    },
    retrieveArticleEN() {
      return this.$axios.get('articlesRetrieveEN').then((res) => {
        this.articles_en = res.data
        console.log(this.articles_en)
      })
    },
    lawRegistrationRW() {
      const data = {
        'article': this.articleSelected,
        'title': this.title
      }
      if (this.title !== null && this.articleSelected !== null){
        this.$axios.post('storeLaw', data).then((res) => {
          this.lawsRetrieve()
        })
      }
    },
    lawsRetrieve() {
      return this.$axios.get('retrieveLaws').then((res) => {
        this.laws = res.data
        this.title = ''
        this.articleSelected = ''
      })
    },
    lawRegistrationFR() {
      const data = {
        'article': this.articleSelected,
        'title': this.title
      }
      if (this.title !== null && this.articleSelected !== null){
        this.$axios.post('storeLawFR', data).then((res) => {
          this.lawsRetrieveFR();
        })
      }
    },
    lawsRetrieveFR(){
      return this.$axios.get('retrieveLawsFR').then((res) => {
        this.laws_fr = res.data
        this.title = ''
        this.articleSelected = ''
      })
    },
    lawRegistrationEN() {
      const article = {
        article: this.articleSelected,
        title: this.title,
      }
      if (this.chapterSelected !== '' && this.title !== '') {
        return this.$axios.post('storeLawEN', article).then((res) => {
          this.lawsRetrieveEN()
          this.articleSelected = ''
          this.title = ''
        })
      }
    },
    lawsRetrieveEN() {
      return this.$axios.get('retrieveLawsEN').then((res) => {
        this.laws_en = res.data
        console.log(this.laws_en)
        this.title = ''
        this.articleSelected = ''
      })
    }
  }
}
</script>

<style scoped>

</style>
