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
                        <v-col cols="12" sm="4" md="4" lg="4" class="pd-0">
                          <p>Kwandika Ingingo</p>
                          <v-select
                            :items="chapter"
                            v-model="chapterSelected"
                            label="Hitamo ingingo"
                            @change="retrieveChapterRW"
                            outlined
                          ></v-select>
                          <v-text-field
                            label="Article Name"
                            placeholder="Article"
                            v-model="title"
                            dense
                            outlined
                          ></v-text-field>
                          <v-btn
                            style="width: 100%"
                            class="mt-1 mb-4 primary"
                            @click="articleRegistrationRW"
                          >Injiza ingingo</v-btn>
                        </v-col>
                        <v-col cols="12" sm="8" md="8" lg="8" class="pd-0">
                          <v-data-table
                            :items="articles"
                            :headers="headerArticles">
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
                        <v-col cols="12" sm="4" md="4" lg="4" class="pd-0">
                          <p>Article Registration</p>
                          <v-select
                            :items="chapters_en"
                            v-model="chapterSelected"
                            label="Hitamo ingingo"
                            @change="retrieveChapterEN"
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
                            class="mt-1 mb-4 secondary"
                            @click="articleRegistrationEN"
                          >Register Article</v-btn>
                        </v-col>
                        <v-col cols="12" sm="8" md="8" lg="8" class="pd-0">
                          <v-data-table
                            :items="articles_en"
                            :headers="headerArticles">
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
                        <v-col cols="12" sm="4" md="4" lg="4" class="pd-0">
                          <p>Chapitre Registration</p>
                          <v-select
                            :items="chapters_fr"
                            v-model="chapterSelected"
                            label="Hitamo ingingo"
                            @change="retrieveChapterEN"
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
                            @click="articleRegistrationFR"
                          >Chapitre Registration</v-btn>
                        </v-col>
                        <v-col cols="12" sm="8" md="8" lg="8" class="pd-0">
                          <v-data-table
                            :items="articles_fr"
                            :headers="headerArticles">
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
    this.retrieveArticle()
    this.retrieveArticleFR()
    this.retrieveChapterRW()
    this.retrieveChapterEN()
    this.retrieveChapterFR()
  },
  data: () => ({
    chapter: [],
    chapters: [],
    chapters_en: [],
    chapters_fr: [],
    sections: [],
    articles: [],
    headerArticles: [
      { text: "#", value:"value"},
      { text: "Articles", value: "text"},
      { text: "Chapters", value: "chapter"},
      { text: "Category", value: "category"}
    ],
    articles_en: [],
    articles_fr: [],
    section: '',
    sousSection: '',
    sectionSelected: '',
    sousSectionSelected: '',
    chapterSelected: '',
    sectionBtn: false,
    sousSectionBtn: false,
    sectionTxt: false,
    sousSectionTxt: false,
    title: '',
    articleBtn: false,
    checkbox: false,
    sousCheckbox: false,
  }),
  methods: {
    articleRegistrationRW() {
      const article = {
        chapterId: this.chapterSelected,
        title: this.title
      }
      if (this.chapterSelected !== '' && this.title !== '') {
        return this.$axios.post('storeArticle', article).then((res) => {
          this.retrieveArticle()
          this.chapterSelected = ''
          this.title = ''
        })
      }
    },
    articleRegistrationEN() {
      const article = {
        chapterId: this.chapterSelected,
        title: this.title,
      }
      if (this.chapterSelected !== '' && this.title !== '') {
        return this.$axios.post('storeArticleEN', article).then((res) => {
          this.retrieveArticleEN()
          this.chapterSelected = ''
          this.title = ''
        })
      }
    },
    articleRegistrationFR() {
      const article = {
        chapterId: this.chapterSelected,
        title: this.title,
      }
      if (this.chapterSelected !== '' && this.title !== '') {
        return this.$axios.post('storeArticleFR', article).then((res) => {
          this.retrieveArticleFR()
          this.chapterSelected = ''
          this.title = ''
        })
      }
    },
    retrieveArticle() {
      return this.$axios.get('articlesRetrieveRW').then((res) => {
        this.articles = res.data
      })
    },
    retrieveArticleEN() {
      return this.$axios.get('articlesRetrieveEN').then((res) => {
        this.articles_en = res.data
        console.log(this.articles)
      })
    },
    retrieveArticleFR() {
      return this.$axios.get('articlesRetrieveFR').then((res) => {
        this.articles_fr = res.data
      })
    },
    retrieveChapterRW() {
      return this.$axios.get('retrievesChaptersRW').then((res) => {
        this.chapter = res.data
        console.log(this.chapter)
      })
    },
    retrieveChapterEN() {
      return this.$axios.get('retrievesChaptersEN').then((res) => {
        this.chapters_en = res.data
        console.log(this.chapters)
      })
    },
    retrieveChapterFR() {
      return this.$axios.get('retrievesChaptersFR').then((res) => {
        this.chapters_fr = res.data
      })
    }
  }
}
</script>

<style scoped>

</style>
