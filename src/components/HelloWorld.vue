<template>
  <v-dialog v-model="dialog" max-width="800px">
    <v-form ref="formProfile">
      <v-card max-width="800px">
        <v-card-title>Profile</v-card-title> <v-divider></v-divider>
        <v-card-text>
          <v-row>
            <v-col cols="12" class="pb-8">
              <v-list-item three-line>
                <v-avatar size="100" color="red">
                  <img :src="imageUrl" height="150" v-if="imageUrl" />
                </v-avatar>
                <v-list-item-content>
                  <v-list-item-title
                    class="pl-9 blue--text text-decoration-underline"
                    label="Select Image"
                    @click="pickFile"
                    v-model="imageName"
                  >
                    Change images
                  </v-list-item-title>
                  <v-list-item-title
                    class="pl-9 blue--text text-decoration-underline"
                    @click="resetImage"
                  >
                    Reset
                  </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
              <input
                type="file"
                style="display: none"
                ref="image"
                accept="image/*"
                @change="onFilePicked"
              />
            </v-col>
            <v-col cols="12" class="ma-0 pa-0 pr-3 pl-3">
              <v-text-field outlined label="Name" v-model="name"></v-text-field>
            </v-col>
            <v-col cols="12" class="ma-0 pa-0 pr-3 pl-3">
              <v-autocomplete
                :items="items_office"
                outlined
                label="Office"
              ></v-autocomplete>
            </v-col>
            <v-col cols="12" class="ma-0 pa-0 pr-3 pl-3">
              <v-select :items="gender" outlined label="Gender"></v-select>
            </v-col>
            <v-col cols="12" class="ma-0 pa-0 pr-3 pl-3">
              <v-menu
                ref="menu"
                transition="scale-transition"
                offset-y
                max-width="290px"
                min-width="290px"
              >
                <template v-slot:activator="{ on, attrs }">
                  <v-text-field
                    outlined
                    v-model="dateBirth"
                    label="Year of Birth"
                    v-bind="attrs"
                    v-on="on"
                  ></v-text-field>
                </template>
                <v-date-picker
                  v-model="dateBirth"
                  type="month"
                  no-title
                  scrollable
                >
                </v-date-picker>
              </v-menu>
            </v-col>
            <v-col cols="12" class="ma-0 pa-0 pr-3 pl-3">
              <v-text-field
                outlined
                label="Email"
                v-model="email"
              ></v-text-field>
            </v-col>
          </v-row>
        </v-card-text>
        <v-card-actions class="pt-0 pb-6 px-4">
          <v-spacer></v-spacer>
          <v-btn
            depressed
            outlined
            width="120"
            class="font-weight-regular"
            :style="{ 'border-color': '#e5e5e5' }"
            @click="dialog = false"
          >
            Cancel
          </v-btn>
          <v-btn depressed width="120" color="primary" @click="dialog = false">
            Save
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-form>
  </v-dialog>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    dialog: true,
    dateBirth: null,
    name: "John Doe",
    items_office: ["DAD", "b", "c", "d"],
    gender: ["male", "female"],
    email: "truong.le241199@gmail.com",

    imageName: "",
    imageUrl: "",
    imageFile: "",
  }),
  methods: {
    pickFile() {
      this.$refs.image.click();
    },

    onFilePicked(e) {
      const files = e.target.files;
      if (files[0] !== undefined) {
        this.imageName = files[0].name;
        if (this.imageName.lastIndexOf(".") <= 0) {
          return;
        }
        const fr = new FileReader();
        fr.readAsDataURL(files[0]);
        fr.addEventListener("load", () => {
          this.imageUrl = fr.result;
          this.imageFile = files[0]; // this is an image file that can be sent to server...
        });
      } else {
        this.imageName = "";
        this.imageFile = "";
        this.imageUrl = "";
      }
    },
    resetImage() {
      (this.imageName = ""),
        (this.imageUrl = ""),
        (this.imageFile = ""),
        this.$refs.formProfile.reset();
    },
  },
};
</script>