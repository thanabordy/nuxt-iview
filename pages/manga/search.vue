<template>
  <div class="container">
    <h1>Manga Search Page</h1>
    <br />
    <Input v-model="query" placeholder="search" style="width: 100%;" />
    <Button type="primary" style="margin-top: 20px;" @click="handdleSearchManga">Search Manga</Button>
    <Divider />
    <Row :gutter="16" type="flex" justify="center" class="code-row-bg">
      <Col v-for="(manga,i) in results" :key="i" style="width: 300px; margin-top: 10px">
        <a @click="handleManageClick(manga)">
          <Card style="height:300px">
            <p slot="title">{{ manga.title }}</p>
            <Row type="flex" justify="center">
              <Col :span="16">
                <p style="width: 100%">{{ manga.synopsis }}</p>
              </Col>
              <Col :span="8">
                <img :src="manga.image_url" alt style="width: 100%;" />
              </Col>
            </Row>
          </Card>
        </a>
      </Col>
    </Row>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      query: 'Dragon',
      results: []
    }
  },
  methods: {
    async handdleSearchManga() {
      // console.log('search manga key', this.query)
      const url = `https://api.jikan.moe/v3/search/manga?q=${this.query}&page=1`
      // console.log('URL', url)
      const response = await axios.get(url)
      // console.log(response)
      this.results = response.data.results
      // console.log('this.results', this.results)
    },
    handleManageClick(manga) {
      // console.log('manga clicked', manga)
      // window.location = manga.url // Will take you to 'manga url'.
      window.open(manga.url) // This will open 'manga url' in a new window.
    }
  }
}
</script>

<style lang="css" scoped>
.container {
  margin: 40px 60px;
}
</style>
