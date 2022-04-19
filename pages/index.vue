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
                          <p>Kwandika Umutwe</p>
                          <v-select
                            :items="categories_rw"
                            v-model="categorySelected"
                            label="Category"
                            return-object
                            outlined
                          ></v-select>
                          <v-text-field
                            label="Chapter Name"
                            placeholder="Chapter Name"
                            v-model="title"
                            dense
                            outlined
                          ></v-text-field>

                          <v-textarea
                            label="DESCRIPTION"
                            placeholder="DESCRIPTION Name"
                            v-model="description"
                            dense
                            outlined
                          ></v-textarea>
                          <v-btn
                            style="width: 100%"
                            class="mt-1 mb-4 primary"
                            @click="chapterRegistrationRW"
                          >Injiza umutwe</v-btn>
                        </v-col>
                        <v-col cols="12" sm="8" md="8" lg="8" class="pd-0">
                          <v-data-table
                            :items="chapters"
                            :headers="headers">
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
                          <p>Chapter Registration</p>
                          <v-select
                            :items="categories_en"
                            v-model="categorySelected"
                            label="Category"
                            return-object
                            outlined
                          ></v-select>
                          <v-text-field
                            label="Chapter Name"
                            placeholder="Chapter Name"
                            v-model="title"
                            dense
                            outlined
                          ></v-text-field>

                          <v-textarea
                            label="DESCRIPTION"
                            placeholder="DESCRIPTION Name"
                            v-model="description"
                            dense
                            outlined
                          ></v-textarea>
                          <v-btn
                            style="width: 100%"
                            class="mt-1 mb-4 secondary"
                            @click="chapterRegistrationEN"
                          >Register Chapter</v-btn>
                        </v-col>
                        <v-col cols="12" sm="8" md="8" lg="8" class="pd-0">
                          <v-data-table
                            :items="chapters_en"
                            :headers="headers">
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
                          <p>Registration Chapitre</p>
                          <v-select
                            :items="categories_fr"
                            v-model="categorySelected"
                            label="Category"
                            return-object
                            outlined
                          ></v-select>
                          <v-text-field
                            label="Chapter Name"
                            placeholder="Chapitre Name"
                            v-model="title"
                            dense
                            outlined
                          ></v-text-field>

                          <v-textarea
                            label="DESCRIPTION"
                            placeholder="DESCRIPTION Name"
                            v-model="description"
                            dense
                            outlined
                          ></v-textarea>
                          <v-btn
                            style="width: 100%"
                            class="mt-1 mb-4 green"
                            @click="chapterRegistrationFR"
                          >Registration</v-btn>
                        </v-col>
                        <v-col cols="12" sm="10" md="10" lg="10" class="pd-0">
                          <v-data-table
                            :items="chapters_fr"
                            :headers="headers">
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
  name: 'IndexPage',
  mounted() {
    // this.chapterRetrieve()
    this.categoryRetrieveFR()
    this.categoryRetrieveEN()
    this.categoryRetrieveRW()
    this.retrieveChapterEN()
    this.retrieveChapterFR()
    this.retrieveChapterRW()
  },
  data: () => ({
    chapter: '',
    chapters:[],
    chapters_en:[],
    chapters_fr:[],
    articles: [],
    categories_fr: [],
    categories_rw: [],
    categories_en: [],
    categorySelected: '',
    description: '',
    tab: null,
    headers: [
      { text: "#", value:"value"},
      { text: "Chapter", value:"text"},
      { text: "Category", value:"category"}
    ],
    headerChapter: [
      { text: "#", value:"value"},
      { text: "Chapters", value: "text"},
    ],
    laws: [],
    article: '',
    title: '',
    sectionShow: false
  }),
  methods: {
    categoryRetrieveFR() {
      return this.$axios.get('categoryRetrieveFR').then((res) => {
        this.categories_fr = res.data
      })
    },
    categoryRetrieveEN() {
      return this.$axios.get('categoryRetrieveEN').then((res) => {
        this.categories_en = res.data
      })
    },
    categoryRetrieveRW() {
      return this.$axios.get('categoryRetrieveRW').then((res) => {
        this.categories_rw = res.data
      })
    },
    chapterRetrieve() {
      return this.$axios.get('retrievesChapters').then((res) => {
        this.chapters = res.data
      })
    },
    retrieveArticle() {
      const section = this.section.value
      const sub = this.subSection.value
      return this.$axios.get('articleRetrieveRW').then((res) => {
        this.articles = res.data
        console.log(res.data)
      })
    },
    retrieveLaws() {
      const chapter = {
        articleId: this.article
      }
      return this.$axios.get('retrieveLaws/' + chapter).then((res) => {
        this.laws = res.data
        console.log(res.data)
      })
    },
    chapterRegistrationRW() {
      const titles = {
        title: this.title,
        category: this.categorySelected.value,
        description: this.description,

      }
      if (this.title !== "") {
        return this.$axios.post('storeChapterRW', titles).then((res) => {
          this.retrieveChapterRW()
          console.log(res.data)
          this.title = ''
          this.description = ''
        })
      }
    },
    chapterRegistrationEN() {
      const titles = {
        title: this.title,
        category: this.categorySelected.value,
        description: this.description,
      }
      if (this.title !== "") {
        return this.$axios.post('storeChapterEN', titles).then((res) => {
          this.retrieveChapterEN()
          console.log(res.data)
          this.title = ''
          this.description = ''
        })
      }
    },
    chapterRegistrationFR() {
      const titles = {
        title: this.title,
        category: this.categorySelected.value,
        description: this.description,
      }
      if (this.title !== "") {
        return this.$axios.post('storeChapterFR', titles).then((res) => {
          this.retrieveChapterFR()
          console.log(res.data)
          this.title = ''
          this.description = ''
        })
      }
    },
    retrieveChapterRW() {
      return this.$axios.get('retrievesChaptersRW').then((res) => {
        this.chapters = res.data
        console.log(this.chapters)
      })
    },
    retrieveChapterEN() {
      return this.$axios.get('retrievesChaptersEN').then((res) => {
        this.chapters_en = res.data
        console.log(this.chapters_en)
      })
    },
    retrieveChapterFR() {
      return this.$axios.get('retrievesChaptersFR').then((res) => {
        this.chapters_fr = res.data
        console.log(this.chapters_fr)
      })
    }
  }
}
</script>
<style scoped>
.input-control {
  margin-top: 100px;
}
</style>
