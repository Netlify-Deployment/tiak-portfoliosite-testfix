<template>
  <bael-grid :posts="groupings" />
</template>

<script>
export default {
  watchQuery: ["page"],

  async asyncData({ params, app, payload, route, store }) {
    await store.commit("SET_TITLE", "Groupings");
  },
  transition(to, from) {
    if (!from) return "fade";
    return +to.query.page > +from.query.page ? "slide-right" : "slide-left";
  },
  data() {
    return {};
  },
  head() {
    return {
      title: "Groupings | " + this.$store.state.info.sitename,
    };
  },
  mounted() {
    this.$store.commit("SET_CURRENT", {
      title: "Groupings",
      dir: ''
    });
  },
  computed: {
    groupings() {
        console.log(this.$store.state.categories);
        console.log(this);
        console.log(this.$store.$router.currentRoute.params.slug);
        var groupTitle = this.$store.$router.currentRoute.params.slug;
        var filteredCategories = [];
        for (var i = 0; i < this.$store.state.categories.length; i++) {
            console.log("Comparison: " + this.$store.state.categories[i].group.toLowerCase() + " VS " + groupTitle.toLowerCase());
            if (this.$store.state.categories[i].group.toLowerCase() == groupTitle.toLowerCase()) {
                filteredCategories.push(this.$store.state.categories[i]);
            }
        }
        return filteredCategories;
      //return this.$store.state.categories;
    },
  },
};
</script>

<style>
.browse a {
  width: 100%;
}
.search:focus {
  outline: none;
}
.footer__heading {
  text-transform: uppercase;
}
nav .r {
  grid-gap: 0;
}
.r.full-height {
  grid-gap: 0;
}
@media only screen and (max-width: 40rem) {
  .xs-collapse {
    visibility: hidden;
    visibility: collapse;
    border: 0 !important;
    border-color: none !important;
    padding: 0 !important;
  }
  .xs-visible {
    visibility: visible;
  }
}
</style>
