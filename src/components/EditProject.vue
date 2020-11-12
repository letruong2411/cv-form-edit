<template>
  <v-dialog v-model="dialog" max-width="800px">
    <v-form>
      <v-card max-width="800px">
        <v-card-title>Profile</v-card-title> <v-divider></v-divider>
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
              <v-autocomplete
                :items="items_positon"
                outlined
                label="Position"
              ></v-autocomplete>
            </v-col>
            <v-col cols="12" class="ma-0 pa-0 pr-3 pl-3">
              <v-text-field
                outlined
                label="Description"
                v-model="description"
              ></v-text-field>
            </v-col>
            <v-col cols="12" class="ma-0 pa-0 pr-3 pl-3">
              <v-text-field
                outlined
                label="Responsibilities"
                v-model="responsibilities"
              ></v-text-field>
            </v-col>
            <v-col cols="12" class="ma-0 pa-0 pr-3 pl-3">
              <v-combobox
                :items="teamSize"
                outlined
                label="Team size"
              ></v-combobox>
            </v-col>
            <v-col cols="12" class="ma-0 pa-0 pr-3 pl-3">
              <v-combobox
                :items="technologies"
                outlined
                multiple
                persistent-hint
                label="Technologies"
              ></v-combobox>
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
    dialog: true,
    dateTo: null,
    dateFrom: null,
    name: "John Doe",
    teamSize: ["1", "2", "3", "4", "5"],
    gender: ["male", "female"],
    items_positon: ["TeamLead", "TeamMentor", "Team"],
    description:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore ",
    responsibilities:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore ",
    technologies: ["Java", "Vue", "React"],
  }),
};
</script>