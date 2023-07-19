<template>
  <div class="col-12 col-md-10 col-lg-7">
    <div class="card textcenter mt-3">
      <div
        class="card-header bg-primary text-white"
        @click="hidepanel = !hidepanel"
      >
        <font-awesome-icon icon="plus" class="mr-3" /> Add Request
      </div>

      <Collapse :when="!hidepanel" class="card-cover">
        <div class="card-body">
          <form id="reqForm" @submit.prevent="requestAdd">
            <div class="form-group form-row">
              <label
                class="col-md-2 col-form-label text-md-right"
                for="classCode"
                >Class Code</label
              >
              <div class="col-md-10">
                <input
                  type="text"
                  class="form-control"
                  name="classCode"
                  v-model="formData.classCode"
                  id="classCode"
                  placeholder="Course's Code / Class's Code"
                />
              </div>
            </div>
            <div class="form-group form-row">
              <label
                class="col-md-2 col-form-label text-md-right"
                for="assignmentValue"
                >Asg. Value</label
              >
              <div class="col-md-10">
                <input
                  type="number"
                  class="form-control"
                  name="assignmentValue"
                  v-model="formData.assignmentValue"
                  id="assignmentValue"
                  placeholder="Pre-paid fee"
                />
              </div>
            </div>
            <div class="form-group form-row">
              <label
                class="col-md-2 col-form-label text-md-right"
                for="assignmentName"
                >Asg. Name</label
              >
              <div class="col-md-10">
                <input
                  type="text"
                  class="form-control"
                  name="assignmentName"
                  v-model="formData.assignmentName"
                  id="assignmentName"
                  placeholder="Assignment's Name"
                />
              </div>
            </div>
            <div class="form-group form-row">
              <label class="col-md-2 col-form-label text-md-right" for="student"
                >Student</label
              >
              <div class="col-md-10">
                <input
                  type="text"
                  class="form-control"
                  id="student"
                  name="student"
                  v-model="formData.student"
                  placeholder="Student"
                />
              </div>
            </div>
            <div class="form-group form-row">
              <label
                class="col-md-2 col-form-label text-md-right"
                for="receivedDate"
                >Date</label
              >
              <div class="col-md-4">
                <input
                  type="date"
                  class="form-control"
                  id="receivedDate"
                  name="receivedDate"
                  v-model="formData.receivedDate"
                />
              </div>
              <label
                class="col-md-2 col-form-label text-md-right"
                for="receivedTime"
                >Time</label
              >
              <div class="col-md-4">
                <input
                  type="time"
                  class="form-control"
                  name="receivedTime"
                  v-model="formData.receivedTime"
                  id="receivedTime"
                />
              </div>
            </div>
            <div class="form-group form-row">
              <label class="col-md-2 text-md-right" for="assignmentNotes"
                >Asg. Notes</label
              >
              <div class="col-md-10">
                <textarea
                  class="form-control"
                  name="assignmentNotes"
                  v-model="formData.assignmentNotes"
                  id="assignmentNotes"
                  rows="4"
                  cols="50"
                  placeholder="Assignment's Notes"
                ></textarea>
              </div>
            </div>
            <div class="form-group form-row">
              <label class="col-md-2 col-form-label text-md-right" for="method"
                >Method</label
              >
              <div class="col-md-10">
                <input
                  type="text"
                  class="form-control"
                  name="method"
                  v-model="formData.method"
                  id="method"
                  placeholder="Method of complete"
                />
              </div>
            </div>
            <div class="form-group form-row mb-0">
              <div class="col-md-10">
                <button type="submit" class="btn btn-primary d-block ml-auto">
                  Add Request
                </button>
              </div>
            </div>
          </form>
        </div>
      </Collapse>
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import { Collapse } from "vue-collapsed";
export default {
  name: "AddRequest",
  data() {
    return {
      hidepanel: true,
      formData: {},
    };
  },
  components: {
    FontAwesomeIcon,
    Collapse,
  },
  methods: {
    requestAdd: function () {
      this.formData = {
        classCode: this.formData.classCode,
        assignmentValue: this.formData.assignmentValue,
        assignmentName: this.formData.assignmentName,
        student: this.formData.student,
        receivedDate:
          this.formData.receivedDate + " " + this.formData.receivedTime,
        assignmentNotes: this.formData.assignmentNotes,
        method: this.formData.method,
      };
    },
  },
};
</script>
<style>
.card-header {
  cursor: pointer;
}
.card-cover {
  transition: height 400ms cubic-bezier(0.3, 0, 0.6, 1);
}
</style>
