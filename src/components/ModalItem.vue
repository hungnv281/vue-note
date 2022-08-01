<template>
  <div>
    <a-modal
      :visible="isShow"
      width="800px"
      title="Basic Modal"
      @ok="onFinish"
      @cancel="endShowModal"
    >
      <a-form>
        <a-form-item
          label="title"
          name="title"
          :labelCol="{ span: 3 }"
          :wrapper-col="{ span: 18 }"
        >
          <a-input
            placeholder="title"
            @change="changeTitle"
            :value="value.title"
          ></a-input>
        </a-form-item>
        <a-form-item
          label="tag"
          name="tag"
          :labelCol="{ span: 3 }"
          :wrapper-col="{ span: 18 }"
        >
          <a-input
            placeholder="tag"
            @change="changeTag"
            :value="value.tag"
          ></a-input>
        </a-form-item>
        <a-form-item
          label="description"
          name="description"
          :wrapper-col="{ span: 18 }"
          :labelCol="{ span: 3 }" 
        >
          <a-textarea
            placeholder="description"
            @change="changeDescription"
            :value="value.description"
            :rows="5"
          ></a-textarea>
        </a-form-item>
      </a-form>
    </a-modal>
  </div>
  <button @click="showdata">123</button>
</template>
<script>
export default {
  name: "ModalItem",
  props: {
    defaultData: Object,
    isShow: Boolean,
    // showModal: Function,
    endShowModal: Function,
    // createNote: Function,
    createNote: Function,
  },
  data() {
    return {
      value: this.defaultData,
    };
  },
  methods: {
    showdata() {
      console.log(this.defaultData);
    },
    onFinish() {
      console.log("Success:", this.value);
      this.createNote(this.value);
    },
    changeTitle(event) {
      this.value = {
        ...this.value,
        title: event.target.value,
      };
    },
    changeDescription(event) {
      this.value = {
        ...this.value,
        description: event.target.value,
      };
    },
    changeTag(event) {
      this.value = {
        ...this.value,
        tag: event.target.value,
      };
    },
  },
};
</script>

<style scoped>
label {
  width: 100px;
}
</style>