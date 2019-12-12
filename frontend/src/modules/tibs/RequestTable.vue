<template>
<v-data-table :headers="headers" :items="request" :search="search" sort-by="calories" absolute class="elevation-1">
    <template v-slot:top>
        <v-toolbar flat class="ma-5 mb-12 pa-5">
            <!-- <v-spacer></v-spacer> -->
            <!-- <v-avatar tile right class="mr-2" size="62">
            <img src="@/assets/pnlogo.png">
          </v-avatar> -->
            <v-toolbar-title class="text-center display-2">Pending Request</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line hide-details></v-text-field>
        </v-toolbar>
    </template>
    <template v-slot:item.action="{ item }">
        <v-btn x-small color="orange" dark>Pending</v-btn>
        <v-btn x-small color="primary" dark>Reject</v-btn>
        <v-btn x-small color="secondary" dark>Approved</v-btn>
    </template>
    <template v-slot:item.info="{ item }">
        <!-- <v-icon small>mdi-information</v-icon> -->
        <v-dialog v-model="dialog" max-width="290">
            <template v-slot:activator="{ on }">
                <v-btn color="primary" dark v-on="on">Open Dialog</v-btn>
            </template>
            <v-card>
                <v-card-title class="headline">Use Google's location service?</v-card-title>
                <v-card-text>Let Google help apps determine location. This means sending anonymous location data to Google, even when no apps are running.</v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="green darken-1" text @click="dialog = false">Disagree</v-btn>
                    <v-btn color="green darken-1" text @click="dialog = false">Agree</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </template>

</v-data-table>
</template>

<script>
export default {
    name: "resquestTable",
    props: ["request"],
    data: () => ({
        search: "",
        dialog2: false,
        dialog: false,
        headers: [{
                text: "Date Of Submission",
                align: "left",
                value: "dateOfSubmit"
            },
            {
                text: "Firstname",
                sortable: false,
                value: "firstname"
            },
            {
                text: "Lastname",
                value: "lastname"
            },
            {
                text: "Category",
                value: "category"
            },
            {
                text: "Nedeed on",
                value: "when"
            },
            {
                text: "Batch",
                value: "batch"
            },
            {
                text: "Actions",
                value: "action",
                sortable: false
            },
            {
                text: "Details",
                value: "info",
                sortable: false
            }
        ]
    }),

    computed: {
        formTitle() {
            return this.editedIndex === -1 ? "New Item" : "Edit Item";
        }
    }

    // watch: {
    //   dialog (val) {
    //     val || this.close()
    //   },
    // },

    // created () {
    //   this.initialize()
    // },

    // methods: {
    //   initialize () {
    //     this.desserts = [
    //       {
    //         firstnname: 'Renzy',
    //         lastname: 'Verano',
    //         category: "Personal",
    //         when: "2019-12-15",
    //         batch: 2021,
    //       }
    //     ]
    //   },

    //   editItem (item) {
    //     this.editedIndex = this.desserts.indexOf(item)
    //     this.editedItem = Object.assign({}, item)
    //     this.dialog = true
    //   },

    //   deleteItem (item) {
    //     const index = this.desserts.indexOf(item)
    //     confirm('Are you sure you want to delete this item?') && this.desserts.splice(index, 1)
    //   },

    //   close () {
    //     this.dialog = false
    //     setTimeout(() => {
    //       this.editedItem = Object.assign({}, this.defaultItem)
    //       this.editedIndex = -1
    //     }, 300)
    //   },

    //   save () {
    //     if (this.editedIndex > -1) {
    //       Object.assign(this.desserts[this.editedIndex], this.editedItem)
    //     } else {
    //       this.desserts.push(this.editedItem)
    //     }
    //     this.close()
    //   },
    // },
};
</script>
