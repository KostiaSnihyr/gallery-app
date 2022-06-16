<template>
  <div class="col-12 col-md-10 col-lg-7 mx-auto">
    <div class="input-group my-3">
      <input
          id="SearchApts"
          placeholder="Search"
          type="text"
          class="form-control"
          aria-label="Search Appointments"
          v-model="searchTerm"
      >
      <div class="input-group-append">
        <button
            type="button"
            class="btn btn-primary dropdown-toggle"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
        >
          Sort by
          <span class="caret"></span>
        </button>
        <div class="dropdown-menu dropdown-menu-right">
          <a href="#" class="dropdown-item d-flex justify-content-between" id="title"
             @click="$emit('requestKey', 'title')"
          >
            Title
          </a>
          <a class="dropdown-item d-flex justify-content-between" href="#" id="author"
             @click="$emit('requestKey', 'author')"
          >
            Author
          </a>
          <a href="#" class="dropdown-item d-flex justify-content-between" id="color"
             @click="$emit('requestKey', 'color')"
          >
            Color
          </a>
          <div class="dropdown-divider" role="separator"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchAppointments",
  data() {
    return {
      searchTerm: ""
    };
  },
  watch: {
    searchTerm: function() {
      this.$emit("searchRecords", this.searchTerm);
    }
  },
  props: ["filterKey"],
};
</script>
