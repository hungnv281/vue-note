<template>
  <div class="abc">
    <a-button class="btn" @click="showModal" type="primary">add</a-button>
    <a-button class="btn" @click="showList()" type="primary">{{
      isShowList ? "hide note" : "show list note"
    }}</a-button>
    <a-input
      class="input"
      type="input"
      placeholder="Search ..."
      @change="handleChange"
      v-bind:value="valueAdd"
      v-on:keyup.enter="addNote()"
    ></a-input>
    <a-list
      :grid="{ gutter: 16, column: 4 }"
      :data-source="data1"
      v-model="data1"
      v-show="isShowList"
      :loading="isLoaded"
    >
      <template #renderItem="{ item }">
        <a-list-item>
          <ItemNote :data="{ item }" @click="showModalChange(item)" />
          <a-button
            class="btn"
            @click="deleteDataFromAxios(item.id)"
            type="primary"
            >delete</a-button
          >
        </a-list-item>
      </template>
    </a-list>

    <ModalItem
      :defaultData="itemChange"
      :isShow="isShow"
      :endShowModal="endShowModal"
      :createNote="handleSubmit"
      v-if="isShow"
    />
  </div>
</template>
<script>
import ModalItem from "./ModalItem.vue";
import axios from "axios";
import ItemNote from "./ItemNote.vue";
export default {
  name: "ABC",
  el: "abc",
  data() {
    return {
      isShowList: false,
      isLoaded: false,
      data1: [],
      valueAdd: "",
      isShow: false,
      link: "https://facebook.com",
      itemChange: {},
    };
  },
  created() {
    this.getDataFromAxios();
  },
  methods: {
    showModal() {
      this.isShow = true;
    },
    showModalChange(item) {
      this.isShow = true;
      this.itemChange = item;
    },
    endShowModal() {
      this.isShow = false;
      // this.itemChange = {};
    },
    showList() {
      this.isShowList = !this.isShowList;
    },
    handleChange(event) {
      this.valueAdd = event.target.value;
    },
    getDataFromAxios() {
      this.isLoaded = true;
      axios
        .get("https://62c53ec5a361f725127e3269.mockapi.io/note")
        .then((response) => {
          this.isLoaded = false;
          // console.log(response.data);
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
        });
    },
    createDataToAxios(value) {
      // this.itemChange = {};
      this.isLoaded = true;
      console.log("addd", value);
      axios
        .post("https://62c53ec5a361f725127e3269.mockapi.io/note", value)
        .then(( ) => {
          this.endShowModal();
          this.isLoaded = false;
          // console.log(response.data);
          this.getDataFromAxios();
        });
    },
    EditDataToAxios(value) {
      this.isLoaded = true;
      console.log("edit ", value);
      axios
        .put("https://62c53ec5a361f725127e3269.mockapi.io/note/" + value.id, value)
        .then(() => {
          this.endShowModal();
          this.isLoaded = false;
          this.getDataFromAxios();
        });
    },
    
  },

  computed: {
    handleSubmit: function() {
        console.log("day la id ", this.itemChange.id);
        if (this.itemChange.id) return this.EditDataToAxios(this.itemChange);
        else return this.createDataToAxios(this.itemChange);
      },
  },
  components: {
    ModalItem,
    ItemNote,
  },
};
</script>

<style scoped>
.abc {
  color: red;
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
</style>