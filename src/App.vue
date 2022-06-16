<template>
  <div id="main-app" class="container">
    <search-pictures
        @searchRecords="searchPictures"
        :filterKey="filterKey"
        @requestKey="changeKey"
    />
    <div>Search results: {{ this.searchResults }}</div>
    <div class="card-deck">
      <gallery-list :pictures="filteredPics"/>
    </div>
  </div>
</template>

<script>
import GalleryList from "./components/GalleryList";
import SearchPictures from "@/components/SearchPictures";
import axios from "axios";

export default {
  name: "MainApp",
  data: function() {
    return {
      pictures: [],
      searchTerms: "",
      filterKey: "all",
      searchResults: 0,

    };
  },
  components: {
    GalleryList,
    SearchPictures
  },
  mounted() {
    axios.get("./data/pictures.json").then(response => {
      this.pictures = response.data
      this.searchResults = this.pictures.length
    });
  },
  computed: {
    filteredPics: function() {
      return this.pictures.filter(item => {
        const pictureData = item[this.filterKey];
        if (this.filterKey === 'all') {
          return (item.title.toLowerCase().match(this.searchTerms.toLowerCase()) ||
              item.author.firstName.toLowerCase().match(this.searchTerms.toLowerCase()) ||
              item.color.toLowerCase().match(this.searchTerms.toLowerCase()))
        } else if (pictureData.firstName) {
          return pictureData.firstName.toLowerCase().match(this.searchTerms.toLowerCase());
        } else {
          return pictureData.toLowerCase().match(this.searchTerms.toLowerCase());
         }
      })
    },
  },
  methods: {
    changeKey: function(value) {
      this.filterKey = value;
    },
    searchPictures: function(terms) {
      this.searchTerms = terms;
    }
  }
};
</script>


