<template>
  <div class="listNote">
    <a-button class="btn" @click="toggleModal" type="primary">Add</a-button>
    <a-button class="btn" @click="showList" type="primary">{{
      isShowList ? "Hide note" : "Show list note"
    }}</a-button>
    <a-list
      class="listNote"
      :data-source="data1"
      :grid="{ gutter: 16, xs: 1, sm: 1, md: 2, xl: 4 }"
      v-model="data1"
      v-show="isShowList"
      :loading="isLoaded"
      :pagination="{
        pageSize: 4,
      }"
      item-layout="vertical"
    >
      <template #renderItem="{ item }">
        <a-list-item>
          <ItemNote :data="{ item }" @click="toggleModal(item)" />
          <a-popconfirm
            title="Are you sure delete this task?"
            ok-text="Yes"
            cancel-text="No"
            @confirm="deleteDataFromAxios(item.id)"
            @cancel="cancel"
          >
            <a-button class="btn btn-delete" type="danger"
              ><delete-filled
            /></a-button>
          </a-popconfirm>
        </a-list-item>
      </template>
    </a-list>

    <ModalItem
      :defaultData="itemChange"
      :isShow="isShow"
      :toggleModal="toggleModal"
      :onSubmit="handleSubmit"
      v-if="isShow"
    />
  </div>
</template>
<script>
import ModalItem from "./ModalItem.vue";
import axios from "axios";
import ItemNote from "./ItemNote.vue";
import { DeleteFilled } from "@ant-design/icons-vue";
import { notification } from "ant-design-vue";

export default {
  name: "ListNote",
  el: "listNote",
  data() {
    return {
      isShowList: false,
      isLoaded: false,
      data1: [],
      isShow: false,
      itemChange: {},
    };
  },
  created() {
    this.getDataFromAxios();
  },
  methods: {
    toggleModal(item) {
      this.isShow = !this.isShow;
      this.itemChange = item;
    },
    showList() {
      this.isShowList = !this.isShowList;
    },
    getDataFromAxios() {
      this.isLoaded = true;
      axios
        .get("https://62c53ec5a361f725127e3269.mockapi.io/note")
        .then((response) => {
          this.isLoaded = false;
          this.data1 = [...response.data];
        });
    },
    deleteDataFromAxios(id) {
      this.isLoaded = true;
      axios
        .delete("https://62c53ec5a361f725127e3269.mockapi.io/note/" + id)
        .then(() => {
          this.getDataFromAxios();
          this.isLoaded = false;
          this.openNotification();
          // alert("Delete done!")
        });
    },
    createDataToAxios(value) {
      this.isLoaded = true;
      axios
        .post("https://62c53ec5a361f725127e3269.mockapi.io/note", value)
        .then(() => {
          this.toggleModal();
          this.isLoaded = false;
          this.getDataFromAxios();
        });
    },
    EditDataToAxios(value) {
      this.isLoaded = true;
      console.log("edit ", value);
      axios
        .put(
          "https://62c53ec5a361f725127e3269.mockapi.io/note/" + value.id,
          value
        )
        .then(() => {
          this.toggleModal();
          this.isLoaded = false;
          this.getDataFromAxios();
        });
    },
    handleSubmit(item) {
      if (item.id) {
        this.EditDataToAxios(item);
      } else {
        this.createDataToAxios(item);
      }
    },
    cancel(e) {
      console.log(e);
    },
    openNotification() {
      notification.success({
        message: "Delete note done!!!",
        onClick: () => {
          console.log("Notification Clicked!");
        },
      });
    },
  },
  // computed: {
  //   filteredPeople() {
  //     if (this.data1) {
  //       return this.data1.filter((data) => {
  //         return data.title.match(this.search);
  //       });
  //     }
  //     return false;
  //   },
  // },
  setup() {},
  components: {
    ModalItem,
    ItemNote,
    DeleteFilled,
  },
};
</script>

<style scoped>
.listNote {
  color: red;
  max-width: 1200px;
  width: 100%;
  margin: 0 auto;
}

.btn {
  margin: 10px auto;
  /* padding: 10px; */
  min-width: 200px;
}
.btn + .btn {
  margin-left: 10px;
}

.item:hover {
  cursor: pointer;
}

.input {
  margin: 0 auto 10px;
  width: 300px;
  display: block;
}
.btn-delete {
  position: absolute;
  top: 0px;
  right: 6px;
  /* padding: 10px; */
  min-width: 20px;
}
</style>