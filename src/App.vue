<template>
  <Navbar :pages="pages" :active-page="activePage"></Navbar>

  <router-view></router-view>
  <!-- <PageViewer v-if="pages.length > 0" :page="pages[activePage]"></PageViewer>

  <create-page @page-created="pageCreated"></create-page> -->
</template>

<script>
import CreatePage from "./components/CreatePage.vue";
import Navbar from "./components/Navbar.vue";
import PageViewer from "./components/PageViewer.vue";

export default {
  components: {
    CreatePage,
    Navbar,
    PageViewer,
  },
  created() {
    this.getPages();

    this.$bus.$on("navbarLinkActivated", (index) => {
      this.activePage = index;
    });
  },
  data() {
    return {
      activePage: 0,
      pages: [],
    };
  },
  methods: {
    async getPages() {
      let res = await fetch("pages.json");
      let data = await res.json();

      this.pages = data;
    },
    pageCreated(pageObject) {
      this.pages.push(pageObject);
    },
  },
};
</script>
