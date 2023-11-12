<template>
  <div class="user">
    <input
      class="search_bar"
      type="search"
      placeholder="Search user"
      v-model="query"
    />
    <h1 class="user_head">User</h1>

    <button
      class="btn btn-primary"
      type="button"
      data-bs-toggle="offcanvas"
      data-bs-target="#offcanvasRight"
      aria-controls="offcanvasRight"
      v-for="user in searchList"
      :key="user.id"
    >
      {{ user.name }}
    </button>

    <div
      class="offcanvas offcanvas-end"
      tabindex="-1"
      id="offcanvasRight"
      aria-labelledby="offcanvasRightLabel"
    >
      <div class="offcanvas-header">
        <h5 id="offcanvasRightLabel">Offcanvas right</h5>
        <button
          type="button"
          class="btn-close text-reset"
          data-bs-dismiss="offcanvas"
          aria-label="Close"
        ></button>
      </div>
      <div class="offcanvas-body">data</div>
    </div>

    <div class="accordion" id="accordionExample">
      <div class="accordion-item" v-for="user in searchList" :key="user.id">
        <h2 class="accordion-header" id="headingOne">
          <button
            class="accordion-button"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#collapseOne"
            aria-expanded="true"
            aria-controls="collapseOne"
          >
            {{ user.name }}
          </button>
        </h2>
        <div
          id="collapseOne"
          class="accordion-collapse collapse show"
          aria-labelledby="headingOne"
          data-bs-parent="#accordionExample"
        >
          <div class="accordion-body">data</div>
        </div>
      </div>
    </div>

    <div class="btn-group-vertical">
      <button
        class="btn btn-primary"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#collapseExample"
        aria-expanded="false"
        aria-controls="collapseExample"
        v-for="user in searchList"
        :key="user.id"
      >
        {{ user.name }}
      </button>
    </div>
    <div class="collapse" id="collapseExample">
      <div class="card card-body">
        Some placeholder content for the collapse component. This panel is
        hidden by default but revealed when the user activates the relevant
        trigger.
      </div>
    </div>
    <!-- <div class="user_list">
      <div class="user_content" v-for="user in searchList" :key="user.id">
        {{ user.name }}
      </div>
    </div> -->
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "UserView",
  data() {
    return {
      users_list: [],
      query: "",
    };
  },
  methods: {
    initialUser() {
      const promi = axios.get("http://localhost/userGet.php");
      promi
        .then((response) =>
          response.data.forEach((item) =>
            this.users_list.push({ id: item.id, name: item.name })
          )
        )
        .catch(function (response) {
          console.log(response);
        });
    },
  },
  computed: {
    searchList() {
      return this.users_list.filter((item) => item.name.includes(this.query));
    },
  },
  created() {
    this.initialUser();
  },
};
</script>
<style>
/* .search_bar {
  height: 35px;
  width: 300px;
  border-radius: 35px;
}
.search_bar::placeholder {
  font-size: large;
}
.user_head {
  background-color: black;
  color: white;
  margin: 0;
  margin-top: 20px;
}
.user_list {
  border: 3px black solid;
  overflow-y: scroll;
  padding: 5px;
  height: 400px;
}
.user_content {
  border: 2px solid #aaaaaa;
  text-align: left;
  margin-bottom: 5px;
  font-size: large;
  cursor: grab;
} */
</style>
