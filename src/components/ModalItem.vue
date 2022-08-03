<template>
  <div>
    <a-modal
      :visible="isShow"
      width="800px"
      :title="titleModal"
      @ok="handleSubmit"
      @cancel="toggleModal({})"
      :okText="okText"
    >
      <a-form>
        <a-form-item
          label="title"
          name="title"
          :labelCol="{ span: 3 }"
          :wrapper-col="{ span: 18 }"
        >
          <a-input placeholder="title" v-model:value="item.title"></a-input>
        </a-form-item>
        <a-form-item
          label="tag"
          name="tag"
          :labelCol="{ span: 3 }"
          :wrapper-col="{ span: 18 }"
        >
          <a-input placeholder="tag" v-model:value="item.tag"></a-input>
        </a-form-item>
        <a-form-item
          label="description"
          name="description"
          :wrapper-col="{ span: 18 }"
          :labelCol="{ span: 3 }"
        >
          <a-textarea
            placeholder="description"
            v-model:value="item.description"
            :rows="5"
          ></a-textarea>
        </a-form-item>
      </a-form>
    </a-modal>
  </div>
</template>
<script>
export default {
  name: "ModalItem",
  props: {
    defaultData: Object,
    isShow: Boolean,
    toggleModal: Function,
    onSubmit: Function,
  },
  data() {
    return {
      titleModal: this.defaultData.id !== undefined ? "Modal edit note":"Modal add note" ,
      okText: this.defaultData.id !== undefined ? "Edit":"Create" ,
      value: this.defaultData,
      item: {
        description: this.defaultData.description,
        title: this.defaultData.title,
        tag: this.defaultData.tag,
        id:this.defaultData.id ? this.defaultData.id : "",
      },
    };
  },
  created(){
    console.log(this.defaultData.id)
  },
  methods: {
    showdata() {
      console.log(this.defaultData);
    },
    handleSubmit() {
      console.log("Success:", this.item);
      this.onSubmit(this.item)
    },
  },
};
</script>

<style scoped>
label {
  width: 100px;
}
</style>