<template>
  <div class="home">
    <b-table
      :data="todos"
      :columns="columns"
      :paginated="isPaginated"
      :per-page="perPage"
      :current-page.sync="currentPage"
      :pagination-simple="isPaginationSimple"
      :pagination-position="paginationPosition"
      :default-sort-direction="defaultSortDirection"
      :pagination-rounded="isPaginationRounded"
      :sort-icon="sortIcon"
      :sort-icon-size="sortIconSize"
      default-sort="user.first_name"
      aria-next-label="Next page"
      aria-previous-label="Previous page"
      aria-page-label="Page"
      aria-current-label="Current page"
      v-if="loaded"
    ></b-table>
    <b-button @click="clickMe">Click Me</b-button>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      loaded: false,
      todos: null,
      isPaginated: true,
      isPaginationSimple: false,
      isPaginationRounded: false,
      paginationPosition: "bottom",
      defaultSortDirection: "asc",
      sortIcon: "arrow-up",
      sortIconSize: "is-small",
      currentPage: 1,
      perPage: 5,
      columns: [
        {
          field: "userId",
          label: "UserId",
          width: "40",
          numeric: true,
        },
        {
          field: "id",
          label: "ID",
          width: "40",
          numeric: true,
        },
        {
          field: "title",
          label: "Title",
        },
        {
          field: "completed",
          label: "Completed",
          centered: true,
        },
      ],
    };
  },
  components: {
    HelloWorld,
  },
  methods: {
    clickMe() {
      this.$buefy.notification.open("Clicked!!");
    },
  },
  async mounted() {
    await axios
      .get("https://jsonplaceholder.typicode.com/todos/")
      .then((result) => {
        this.todos = result.data;
        console.log(this.todos);
        this.loaded = true;
      });
  },
};
</script>
