<template>
  <a-card hoverable style="width: 300px">
    <template #cover>
      <img
        alt="example"
        src="https://gw.alipayobjects.com/zos/rmsportal/JiqGstEfoWAOHiTxclqi.png"
      />
    </template>
    <template #actions>
      <setting-outlined key="setting" />
      <edit-outlined key="edit" />
      <ellipsis-outlined key="ellipsis" />
    </template>
    <a-card-meta  :title="data?.item?.title" description="This is the description">
      <template #avatar>
        <a-avatar src="https://joeschmoe.io/api/v1/random" /> 
      </template>
    </a-card-meta>
  </a-card>
  <!-- {{data}} -->
</template>
<script>
import {
  SettingOutlined,
  EditOutlined,
  EllipsisOutlined,
} from "@ant-design/icons-vue";

export default {
  name: "ItemNote",
  components: {
    SettingOutlined,
    EditOutlined,
    EllipsisOutlined,
  },
  created(){
    this.title = this.data?.item?.title
  },
  data() {
    return (
      {
        title: ""
      }
    )
  },
  props: {
    data: Object,
  },
};
</script>