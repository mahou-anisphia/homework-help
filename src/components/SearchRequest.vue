<template>
  <div class="col-12 col-md-10 col-lg-7">
    <div class="input-group my-3">
      <input
        id="SearchApts"
        placeholder="Search"
        type="text"
        class="form-control"
        aria-label="Search Requests"
        v-model="searchTerm"
      />

      <div class="input-group-append">
        <button
          type="button"
          class="btn btn-primary dropdown-toggle"
          data-bs-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          Sort by
          <span class="caret"></span>
        </button>

        <div class="dropdown-menu dropdown-menu-right">
          <a
            href="#"
            class="dropdown-item d-flex justify-content-between"
            id="classCode"
            @click="$emit('requestKey', 'classCode')"
          >
            Class's Code
            <font-awesome-icon icon="check" v-if="srcKey === 'classCode'" />
          </a>

          <a
            class="dropdown-item d-flex justify-content-between"
            href="#"
            id="receivedDate"
            @click="$emit('requestKey', 'receivedDate')"
          >
            Date
            <font-awesome-icon icon="check" v-if="srcKey === 'receivedDate'" />
          </a>

          <a
            href="#"
            class="dropdown-item d-flex justify-content-between"
            id="student"
            @click="$emit('requestKey', 'student')"
          >
            Student
            <font-awesome-icon icon="check" v-if="srcKey === 'student'" />
          </a>

          <div class="dropdown-divider" role="separator"></div>

          <a
            class="dropdown-item d-flex justify-content-between"
            href="#"
            id="asc"
            @click="$emit('requestDir', 'asc')"
          >
            Asc
            <font-awesome-icon icon="check" v-if="srcDir === 'asc'" />
          </a>

          <a
            class="dropdown-item d-flex justify-content-between"
            href="#"
            id="desc"
            @click="$emit('requestDir', 'desc')"
          >
            Desc
            <font-awesome-icon icon="check" v-if="srcDir === 'desc'" />
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
export default {
  name: "SearchRequest",
  data() {
    return {
      searchTerm: "",
    };
  },
  components: {
    FontAwesomeIcon,
  },
  watch: {
    searchTerm: function () {
      this.$emit("searchkey", this.searchTerm);
    },
  },
  props: ["srcKey", "srcDir"],
};
</script>
