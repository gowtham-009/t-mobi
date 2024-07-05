<template>
  <div>
    <div class="container w-100 h-screen d-flex flex-column ga-2">
      <div class="boxex">
       <logo/>
      </div>
      <div class="boxex h-screen bg-green-lighten-1 rounded-t-xl">
        <v-card class="rounded-t-xl">
          <v-tabs v-if="showMainContent" v-model="tab" align-tabs="center" bg-color="green-lighten-1" stacked>
            <v-tab value="tab-1">ID</v-tab>
            <v-tab value="tab-2">Name</v-tab>
            <v-tab value="tab-3">Mobile Number</v-tab>
          </v-tabs>

          <v-tabs-window v-if="showMainContent" v-model="tab">
            <v-tabs-window-item value="tab-1">
              <v-card>
                <div class="main_id_box">
                  <v-sheet class="w-100">
                    <div class="pa-2 bg-green-lighten-1">
                      <v-chip-group selected-class="text-primary" column class="pa-2">
                        <v-chip
                          class="text-white bg-red"
                          v-for="tag in tags"
                          :key="tag"
                          @click="selectTag(tag)"
                        >
                          {{ tag }}
                        </v-chip>
                      </v-chip-group>
                    </div>
                  </v-sheet>
                  <v-sheet class="w-100 pa-2 mt-2">
                    <v-form @submit.prevent="toggleSearch">
                      <v-text-field
                        v-model="idnumber"
                        :rules="rules"
                        label="ID number last four characters"
                      ></v-text-field>
                      <v-btn class="mt-3 bg-deep-purple-accent-4" size="x-large" type="submit" block>Search</v-btn>
                    </v-form>
                  </v-sheet>
                </div>
              </v-card>
            </v-tabs-window-item>

            <v-tabs-window-item value="tab-2" v-if="tab === 'tab-2'">
              <v-card>
                <v-sheet class="w-100 pa-2">
                  <v-form @submit.prevent="namesearch" >
                    <v-text-field v-model="name" label="Name (type min 3 characters)"></v-text-field>
                    <v-text-field v-model="place" label="Place (type min 3 characters)"></v-text-field>
                    <v-btn class="mt-10 bg-deep-purple-accent-4" size="x-large" type="submit" block>Search</v-btn>
                  </v-form>
                </v-sheet>
              </v-card>
            </v-tabs-window-item>

            <v-tabs-window-item value="tab-3" v-if="tab === 'tab-3'">
              <v-card>
                <v-sheet class="w-100 pa-2">
                  <v-form @submit.prevent="phone_loan_search">
                    <v-text-field v-model="mobile" label="Mobile (type min 5 characters)"></v-text-field>
                    <v-text-field v-model="loan" label="Loan (type min 5 characters)"></v-text-field>
                    <v-btn class="mt-10 bg-deep-purple-accent-4" size="x-large" type="submit" block>Search</v-btn>
                  </v-form>
                </v-sheet>
              </v-card>
            </v-tabs-window-item>
          </v-tabs-window>

          <!-- Show only ID card search content -->
          <div v-if="showSearch" class="w-100 pa-2 search_c d-flex ga-2 flex-column justify-center align-center">
            <v-sheet class="mx-auto" width="300">
              <v-form @submit.prevent>
                <h3 class="text-center">Search for result ID</h3>
                <div class="editbox mt-3 d-flex ga-3 justify-center">
                  <v-text-field v-model="searchResult" :label="'Search result for ' + selectedTag"></v-text-field>
                  <v-btn size="x-large" class="bg-yellow" @click="editResult_id">Edit</v-btn>
                </div>
              </v-form>
            </v-sheet>
          </div>
        </v-card>

        <!-- Only show namecontain class content -->
        <div class="namecontain bg-white" v-if="showNameContain">
          <h4 class="text-center">Search Results for Name</h4>
          <div class="name-contain w-100 d-flex ga-1 pa-2 mt-3">
            <div class="w-100 pa-2">
              <v-sheet>
                <v-form fast-fail @submit.prevent class="d-flex w-100 ga-2">
                  <div class="form-field w-75">
                    <v-text-field v-model="resultName" label="Search Result For Name"></v-text-field>
                    <v-text-field v-model="resultPlace" label="Search Result For Place"></v-text-field>
                  </div>
                  <div class="field-btn w-25 d-flex justify-center align-end">
                    <v-btn class="bg-yellow mb-5" size="x-large" type="submit" @click="editResult_name" block>Edit</v-btn>
                  </div>
                </v-form>
              </v-sheet>
            </div>
          </div>
        </div>

        <!-- only show mobileloan class content -->
        <div class="mobile_container w-100 bg-white pa-2" v-if="showMobileContain">
          <h4 class="text-center">Search Results for Phone and loan</h4>
          <div class="name-contain w-100 d-flex ga-1 pa-2 mt-3">
            <div class="w-100 pa-2">
              <v-sheet>
                <v-form fast-fail @submit.prevent class="d-flex w-100 ga-2">
                  <div class="form-field w-75">
                    <v-text-field v-model="mobileResult" label="Search result for phone"></v-text-field>
                    <v-text-field v-model="loanResult" label="Search result for loan"></v-text-field>
                  </div>
                  <div class="field-btn w-25 d-flex justify-center align-end">
                    <v-btn class="bg-yellow mb-5" size="x-large" type="submit" @click="editResult_mobile" block>Edit</v-btn>
                  </div>
                </v-form>
              </v-sheet>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import logo from "~/components/logo.vue"
export default {
  components:{
    logo
  },
  data() {
    return {
      tab: 'tab-1',
      showSearch: false,
      showMainContent: true,
      showNameContain: false,
      showMobileContain:false,
      selectedTag: '',
      tags: [
        'Aadhaar',
        'Voter ID',
        'Driving License',
        'Mnrega',
        'Bank Passbook',
        'Other',
      ],
      idnumber: '',
      rules: [
        value => !!value || 'Required.',
        value => (value && /^\d{4}$/.test(value)) || 'Must be 4 digits',
      ],
      name: '',
      place: '',
      mobile: '',
      loan: '',
      resultName: '', // This will hold the search result for Name
      resultPlace: '', // This will hold the search result for Place
      searchResult: '', // This will hold the value to be displayed in search_c
      mobileResult:'',
      loanResult:''
    };
  },
  methods: {
    selectTag(tag) {
      this.selectedTag = tag;
    },
    toggleSearch() {
      if (this.selectedTag === 'Aadhaar') {
        if (this.idnumber && /^\d{4}$/.test(this.idnumber)) {
          this.searchResult = this.idnumber; // Assigning idnumber to searchResult
          this.showSearch = true;
          this.showMainContent = false;
        } else {
          alert('Please enter a valid 4-digit ID number.');
        }
      } else {
        alert('Please select an ID type first.');
      }
    },
    editResult_id() {
      this.showSearch = false; // Hide search_c
      this.showMainContent = true; // Show main content
      this.tab = 'tab-1'; // Switch to the "ID" tab
    },
    namesearch() {
      if (this.name.length >= 3 && this.place.length >= 3) {
        this.resultName = this.name; // Assigning name to resultName
        this.resultPlace = this.place; // Assigning place to resultPlace
        this.showNameContain = true; // Display namecontain on successful search
        this.showMainContent = false; // Hide tabs and form in tab-2
      } else {
        alert('Please enter at least 3 characters for both Name and Place.');
      }
    },
    editResult_name() {
      this.showNameContain = false; // Hide namecontain class
      this.showMainContent = true; // Show tabs and form in tab-2
      this.tab = 'tab-2'; // Switch to the "Name" tab
    },
    phone_loan_search(){
      if (this.mobile.length >= 5 && this.loan.length >= 5){
          this.mobileResult=this.mobile;
          this.loanResult=this.loan;
          this.showMainContent=false;
          this.showMobileContain=true;
      }
      else{
        alert('please enter at least 5 characters for both phone and loan')
      }
    },
    editResult_mobile(){
      this.showMobileContain=false;
      this.showMainContent=true;
      this.tab = 'tab-3';
    }

  },
};
</script>

<style>
.box1 {
  height: 100px;
}
</style>
