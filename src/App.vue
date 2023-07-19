<template>
  <div id="name-app" class="container">
    <div class="row justify-content-center">
      <add-request @add="addItem" />
      <search-request
        @searchkey="searchRequest"
        :srcKey="filterKey"
        :srcDir="filterDirection"
      />
      <request-list
        :requests="filtered"
        @remove="removeData"
        @edit="editReq"
      ></request-list>
    </div>
  </div>
</template>

<script>
//use for import from file export multiple modules
import RequestList from "./components/RequestList.vue";
import AddRequest from "./components/AddRequest.vue";
import SearchRequest from "./components/SearchRequest.vue";
//use for import file export 1 module or catch the default export; .vue is optional
import axios from "axios";
import _ from "lodash";

export default {
  name: "nameApp",
  data() {
    return {
      requests: [],
      reqIndex: 0,
      reqHideDetails: false,
      searchTerm: "",
      filterKey: "classCode",
      filterDirection: "asc",
    };
  },
  components: {
    RequestList,
    AddRequest,
    SearchRequest,
  },
  mounted() {
    axios.get("./data/data.json").then(
      (response) =>
        (this.requests = response.data.map((item) => {
          item.reqIndex = this.reqIndex;
          item.reqHideDetails = this.reqHideDetails;
          this.reqIndex++;
          return item;
          //adding static id for elements since it will be changed afterward
        }))
    );
  },
  methods: {
    removeData: function (data) {
      this.requests = _.without(this.requests, data);
    },
    editReq: function (id, field, text) {
      const reqIndex = _.findIndex(this.requests, {
        reqIndex: id,
      });
      this.requests[reqIndex][field] = text;
    },
    addItem: function (request) {
      (request.reqIndex = this.reqIndex),
        this.reqIndex++,
        this.requests.push(request);
    },
    searchRequest: function (key) {
      this.searchTerm = key;
    },
  },
  computed: {
    searchReqs: function () {
      return this.requests.filter((item) => {
        return (
          item.assignmentName
            .toLowerCase()
            .match(this.searchTerm.toLowerCase()) ||
          item.student.toLowerCase().match(this.searchTerm.toLowerCase()) ||
          item.assignmentNotes
            .toLowerCase()
            .match(this.searchTerm.toLowerCase())
        );
      });
    },
    filtered: function () {
      return _.orderBy(
        this.searchReqs,
        (item) => {
          return item[this.filterKey].toLowerCase();
        },
        this.filterDirection
      );
    },
  },
};
</script>

<style>
[v-cloak] {
  display: none;
}
</style>
