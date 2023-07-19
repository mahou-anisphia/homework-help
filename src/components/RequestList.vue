<template>
  <div class="col-12 col-md-10 col-lg-7">
    <div class="list-group list-group-flush">
      <div
        class="list-group-item d-flex align-items-start"
        v-for="item in requests"
        :key="item.reqIndex"
      >
        <button
          class="mr-2 btn btn-sm btn-danger"
          @click="$emit('remove', item)"
        >
          <font-awesome-icon icon="trash" />
        </button>
        <div class="w-100">
          <div class="justify-content-between d-flex">
            <span class="h4 text-primary" v-cloak>{{ item.classCode }}</span>
            <span
              class="float-right"
              v-cloak
              contenteditable="true"
              spellcheck="false"
              @blur="
                $emit(
                  'edit',
                  item.reqIndex,
                  'assignmentName',
                  $event.target.innerText
                )
              "
              >{{ item.assignmentName }}</span
            >
            <span class="float-right" v-cloak>{{
              formattedDate(item.receivedDate)
            }}</span>
          </div>
          <div
            class="btn btn-primary"
            @click="item.reqHideDetails = !item.reqHideDetails"
          >
            <font-awesome-icon icon="plus" class="mr-3 more-details" /> More
            Details
          </div>
          <Collapse :when="item.reqHideDetails" class="card-cover">
            <div>
              <span class="text-primary font-weight-bold mr-1"
                >Student ordered:
              </span>
              <span
                v-cloak
                class="owner-name"
                contenteditable="true"
                spellcheck="false"
                @blur="
                  $emit(
                    'edit',
                    item.reqIndex,
                    'student',
                    $event.target.innerText
                  )
                "
                >{{ item.student }}</span
              >
            </div>
            <div>
              <span class="text-primary">Notes/Details: </span>
              <span
                v-cloak
                contenteditable="true"
                spellcheck="false"
                @blur="
                  $emit(
                    'edit',
                    item.reqIndex,
                    'assignmentNotes',
                    $event.target.innerText
                  )
                "
                >{{ item.assignmentNotes }}</span
              >
            </div>
            <div v-cloak>
              <span class="text-primary">Credit Value:</span>
              {{ item.assignmentValue }}
            </div>
            <div v-cloak>
              <span class="text-danger">Method:</span> {{ item.method }}
            </div>
          </Collapse>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import moment from "moment";
import { Collapse } from "vue-collapsed";

export default {
  data() {
    return {
      hideDetails: [],
    };
  },
  name: "RequestList",
  props: ["requests"],
  components: {
    FontAwesomeIcon,
    Collapse,
  },
  methods: {
    formattedDate: (date) => {
      return moment(new Date(date)).format("DD-MM-YY, h:mm a");
    },
  },
};
</script>
<style>
[contenteditable="true"]:hover {
  box-shadow: 0 0 5px rgba(0, 0, 255, 0.7);
}
.more-details {
  cursor: pointer;
}
</style>
