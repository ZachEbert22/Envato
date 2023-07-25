<template>
  <the-navbar
    :pages="pages"
    :active-page="activePage"
    :nav-link-click="(index) => activePage = index"
    ></the-navbar>

      <div v-show = "false">
      hide this content
      </div>

    <page-viewer
        v-if="pages.length > 0"
        :page="pages[activePage]"
    ></page-viewer>
</template>


<script>

import PageViewer from './components/PageViewer.vue';
import TheNavbar from './components/TheNavbar.vue';

export default{
  components: {
    PageViewer,
    TheNavbar,
  },
  created() {
    this.getPages();
  },
  data(){
    return{
      activePage: 0,
      //theme: 'light',
      pages: [],
    };
  },
  methods: {
    async getPages() {
      let res = await fetch('pages.json');
      let data = await res.json();

      this.pages = data;
      //return data;

    }
  }
}
</script>