<template>
  <div>
    <h3 class="my-2 font-weight-regular">Browser all our books!</h3>
    <v-data-table :headers="headers" :items="items" class="elevation-1">
      <template v-slot:top>
        <v-dialog v-model="dialogView" width="250px">
          <v-card max-width="250px">
            <img :src="imageURL" style="width: 100%; height: auto" />
            <v-card-actions class="mt-0">
              <v-spacer></v-spacer>
              <v-btn text @click="dialogView = false">Close</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogEdit" max-width="350px">
          <v-card>
            <v-card-title class="text-h6 font-weight-regular"
              >Edit Book</v-card-title
            ><v-card-text>
              <v-text-field
                v-model="editName"
                label="Name"
                color="teal lighten-1"
                class="my-2"
              ></v-text-field>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="teal lighten-1" text @click="dialogEdit = false"
                >Cancel</v-btn
              >
              <v-btn color="teal lighten-1" text @click="editValue">Save</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </template>
      <template v-slot:item.title="{ item }">
        <p class="font-weight-bold">{{ item.title }}</p>
      </template>
      <template v-slot:item.imageLink="{ item }">
        <img :src="item.imageLink" @click="viewImage(item)" />
      </template>
      <template v-slot:item.actions="{ item }">
        <v-icon
          small
          color="teal lighten-1"
          class="mr-2"
          @click="editItem(item)"
        >
          mdi-pencil
        </v-icon>
        <v-icon
          small
          color="deep-orange darken-1"
          class="mr-1"
          @click="deleteItem(item)"
        >
          mdi-delete
        </v-icon>
      </template>
    </v-data-table>
  </div>
</template>

<script>
export default {
  name: 'Home',

  data() {
    return {
      headers: [
        {
          text: 'Title',
          value: 'title',
        },
        {
          text: 'Image',
          value: 'imageLink',
        },
        {
          text: 'Country',
          value: 'country',
        },
        {
          text: 'Language',
          value: 'language',
        },
        {
          text: 'Actions',
          value: 'actions',
          sortable: false,
          align: 'center',
        },
      ],

      dialogView: false,
      imageURL: null,

      dialogEdit: false,
      editID: null,
      editName: '',
    };
  },
  props: {
    books: {
      type: Array,
    },
  },

  created() {
    this.items = this.books;
  },

  methods: {
    viewImage(item) {
      this.imageURL = item.imageLink;
      this.dialogView = true;
    },

    editItem(item) {
      this.editID = item.id;
      this.editName = item.title;
      this.dialogEdit = true;
    },
    editValue() {
      const item = this.items.find((el) => el.id == this.editID);
      item.title = this.editName;
      this.dialogEdit = false;
    },

    deleteItem(item) {
      const index = this.items.indexOf(item);
      this.items.splice(index, 1);
    },
  },
};
</script>

<style scoped>
img {
  height: 150px;
}
</style>
