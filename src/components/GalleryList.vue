<template>
  <div
      class="card"
      v-for="picture in pictures"
      :key="picture.id"
      style="min-width: 350px; max-width: 350px;"
  >
    <img :src="picture.image" class="card-img-top" alt="item.description">
    <div class="card-body">
      <h5 class="card-title">title: {{picture.title}}</h5>
      <p class="card-description">description: {{picture.description}}</p>
      <p class="card-amount">amount: {{picture.amount}}</p>
      <p class="card-color">color: {{picture.color}}</p>
      <p class="card-author">author: {{picture.author.firstName}} {{picture.author.lastName}}</p>
      <div> tags:
        <ul class="card-tags">
          <li
              v-for="tag in picture.tags"
              :key="picture.id + tag"
          >
            {{ tag }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "GalleryList",
  props: ["pictures"],
  components: {
  },
  methods: {

  }
};
</script>

<style>
  .card {
    margin: 20px;
  }
</style>

