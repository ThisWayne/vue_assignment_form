<template>
  <form class="my-1" v-on:submit.prevent>
    <div class="form-group">
      <label for="personalInfoFirstName">First name</label>
      <input id="personalInfoFirstName" class="form-control" v-model="personalInfo.first_name">
      <label for="personalInfoLastName">Last name</label>
      <input id="personalInfoLastName" class="form-control" v-model="personalInfo.last_name">
    </div>
    <div class="d-flex flex-row">
      <span>Gender</span>
      <div class="d-flex flex-column ml-3">
        <label class="mx-1">
          <input type="radio" value="0" v-model="personalInfo.gender">
          Secret
        </label>
        <label class="mx-1">
          <input type="radio" value="1" v-model="personalInfo.gender">
          Male
        </label>
        <label class="mx-1">
          <input type="radio" value="2" v-model="personalInfo.gender">
          Female
        </label>
      </div>
    </div>
    <div class="form-group">
      <label for="personalInfoAddress">Address</label>
      <input
        id="personalInfoAddress"
        class="form-control"
        v-model="personalInfo.address"
        v-bind:disabled="personalInfo.is_homeless"
      >
      <label class="my-1">
        <input
          type="checkbox"
          v-model="personalInfo.is_homeless"
          v-on:click="$emit('onNoFixedAddressClick')"
        >
        This client has no fixed address
      </label>
    </div>
    <div class="form-group">
      <label for="personalInfoJob">
        Job
        <select
          id="personalInfoJob"
          class="form-control"
          v-bind:value="personalInfoJobValue"
          v-on:change="$emit('onJobSelectChange', $event)"
        >
          <option
            v-for="jobOption in jobOptions"
            v-bind:key="jobOption.value"
            v-bind:value="jobOption.value"
          >{{jobOption.name}}</option>
        </select>
      </label>
    </div>
    <div class="form-group">
      <label for="personalInfoNote">
        Note
        {{noteLength}}/2000 characters
      </label>
      <textarea
        maxlength="2000"
        id="personalInfoNote"
        class="form-control"
        v-bind:value="personalInfo.note"
        v-on:input="$emit('onNoteInput', $event)"
      ></textarea>
    </div>
  </form>
</template>
<script>
const jobOptions = [
  {
    name: "Secret",
    value: ""
  },
  {
    name: "Agent",
    value: "agent"
  },
  {
    name: "Secret Agent",
    value: "secret_agent"
  },
  {
    name: "Agent of Secret Agent",
    value: "agent_of_secret_agent"
  }
];

export default {
  props: {
    personalInfo: {
      type: Object,
      required: true,
      default() {
        return {};
      }
    }
  },
  data() {
    return {
      jobOptions: jobOptions
    };
  },
  computed: {
    noteLength() {
      const { note } = this.$props.personalInfo;
      return note ? note.length : 0;
    },
    personalInfoJobValue() {
      return this.$props.personalInfo.job ? this.$props.personalInfo.job : "";
    }
  }
};
</script>