<template>
  <v-dialog v-model="dialog" max-width="800px">
    <v-form>
      <v-card max-width="800px">
        <v-card-title>Work History</v-card-title> <v-divider></v-divider>
        <v-card-text>
          <v-row>
            <v-col cols="12" class="ma-0 pa-0 pr-3 pl-3">
              <v-text-field outlined label="Name" v-model="name"></v-text-field>
            </v-col>

            <v-col cols="6" class="ma-0 pa-0 pr-3 pl-3">
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
                    v-model="dateTo"
                    label="To"
                    v-bind="attrs"
                    v-on="on"
                  ></v-text-field>
                </template>
                <v-date-picker
                  v-model="dateTo"
                  type="month"
                  no-title
                  scrollable
                >
                </v-date-picker>
              </v-menu>
            </v-col>
            <v-col cols="6" class="ma-0 pa-0 pr-3 pl-3">
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
                    v-model="dateFrom"
                    label="From"
                    v-bind="attrs"
                    v-on="on"
                  ></v-text-field>
                </template>
                <v-date-picker
                  v-model="dateFrom"
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
                label="Company"
                v-model="company"
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
          <v-btn depressed width="120" color="red" class="white--text">
            Delete
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
  name: "EditProject",
  data: () => ({
    dateTo: null,
    dateFrom: null,
    dialog: true,
    name: "John Doe",
    company: "Hybrid Technologies",
  }),
};
</script>