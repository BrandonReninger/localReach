<template>
  <div class="about text-center">
    <h1>Add Organization</h1>
    <!-- <img class="rounded" :src="profile.picture" alt /> -->
    <p>{{ profile.email }}</p>

    <!-- <form @submit.prevent="changeProfile()">
      <div class="form-group">
        <label for="title">Name</label>
        <input
          type="text"
          name="title"
          id
          class="form-control"
          placeholder="enter name..."
          aria-describedby="helpId"
          v-model="profile.name"
          required
        />
      </div>
      <div class="form-group">
        <label for="body">Location</label>
        <input
          type="text"
          name="body"
          id
          class="form-control"
          placeholder="enter Location..."
          aria-describedby="helpId"
          v-model="profile.location"
        />
      </div>
      <div class="form-group">
        <label for="body">payment</label>
        <input
          type="text"
          name="body"
          id
          class="form-control"
          placeholder="enter payment..."
          aria-describedby="helpId"
          v-model="profile.payment"
        />
      </div>
      <div class="form-group">
        <label for="body">picture</label>
        <input
          type="text"
          name="body"
          id
          class="form-control"
          placeholder="enter picture..."
          aria-describedby="helpId"
          v-model="profile.picture"
          required
        />
      </div>
      <div class="form-group">
        <label for="body">default</label>
        <input
          type="text"
          name="body"
          id
          class="form-control"
          placeholder="enter default donation amount..."
          aria-describedby="helpId"
          v-model="profile.default"
          required
        />
      </div>
      <button type="submit" class="btn btn-success">Save</button>
    </form>-->

    <!-- Button trigger modal -->
    <button
      type="button"
      class="btn btn-primary"
      data-toggle="modal"
      data-target="#exampleModal"
    >Organization</button>

    <!-- Modal -->
    <div
      class="modal fade"
      id="exampleModal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog text-center" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Add Organization</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <form class="mb-3" @submit.prevent="addOrg">
              <div class="form-group" v-show="newOrg.name == orgApiData.name">
                <label for="body">EIN:</label>
                <input
                  type="text"
                  name="body"
                  id
                  class="form-control"
                  placeholder="enter EIN..."
                  aria-describedby="helpId"
                  v-model="newOrg.EIN"
                  required
                />
                <button class="btn btn-primary mt-2 btn-block" @click="checkEin()">Check EIN</button>
              </div>

              <div v-show="newOrg.name !== orgApiData.name">
                <!-- <h5 class="m-1 pr-2 pl-3 tskName">Name:</h5>
                <input
                  class="pr-4 pl-2 inputTask"
                  type="text"
                  placeholder="add name of organization..."
                  v-model="orgApiData.name"
                  required
                  disabled
                /> -->

                <div class="form-group">
                  <label for="body">Name:</label>
                  <input
                    type="text"
                    name="body"
                    id
                    class="form-control"
                    placeholder="enter name..."
                    aria-describedby="helpId"
                    v-model="orgApiData.name"
                  />
                </div>
                <div class="form-group">
                  <label for="body">Address:</label>
                  <input
                    type="text"
                    name="body"
                    id
                    class="form-control"
                    placeholder="enter address..."
                    aria-describedby="helpId"
                    v-model="address"
                  />
                </div>

                <div class="form-group">
                  <label for="body">PayPal Client ID:</label>
                  <input
                    type="text"
                    name="body"
                    id
                    class="form-control"
                    placeholder="enter client ID..."
                    aria-describedby="helpId"
                    v-model="newOrg.clientId"
                  />
                </div> 

                <div class="form-group">
                  <label for="body">Email:</label>
                  <input
                    type="text"
                    name="body"
                    id
                    class="form-control"
                    placeholder="enter email..."
                    aria-describedby="helpId"
                    v-model="newOrg.email"
                  />
                </div>

                <div class="form-group">
                  <label for="body">Website:</label>
                  <input
                    type="text"
                    name="body"
                    id
                    class="form-control"
                    placeholder="enter website link..."
                    aria-describedby="helpId"
                    v-model="newOrg.website"
                  />
                </div>

                <div class="form-group">
                  <label for="body">Picture:</label>
                  <input
                    type="text"
                    name="body"
                    id
                    class="form-control"
                    placeholder="enter picture..."
                    aria-describedby="helpId"
                    v-model="newOrg.picture"
                  />
                </div>

                <div class="form-group">
                  <label for="body">Links:</label>
                  <input
                    type="text"
                    name="body"
                    id
                    class="form-control"
                    placeholder="enter social media links..."
                    aria-describedby="helpId"
                    v-model="newOrg.links"
                  />
                </div>

              </div>
            </form>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            <button
              type="button"
              class="btn btn-primary"
              data-dismiss="modal"
              @click="addOrg"
            >Submit</button>
          </div>
        </div>
      </div>
    </div>
    <!-- <org></org> -->
    <!-- <h1>Donation Total: {{ donationTotal }}</h1> -->
    <!-- <DonationDetails
      class=""
      v-for="donationItem in donations"
      :donationData="donationItem"
      :key="donationItem._id"
    ></DonationDetails>-->
  </div>
</template>

<script>
//inport Org from ".."
//import DonationDetails from "../components/DonationDetails.vue";
//import Org from "../components/Org.vue";
export default {
  name: "AddOrg",
  data() {
    return {
      newOrg: {},
      address: ""
    };
  },
  computed: {
    profile() {
      return this.$store.state.profile;
    },
    orgApiData() {
      console.log("orgApiData",this.$store.state.orgApiData )
      let data = this.$store.state.orgApiData
      this.address = data.address + ", " + data.city + ", " + data.state + " " + data.zipcode
      console.log(this.address)
      return this.$store.state.orgApiData;
    }
  },
  mounted() {
    //  this.$store.dispatch("getDonations");
  },
  methods: {
    addOrg() {
      console.log("addOrg", this.newOrg);
      this.newOrg.name = this.orgApiData.name;
      this.newOrg.address = this.orgApiData.address;
      this.$store.dispatch("addOrg", this.newOrg);
      this.newOrg = {};
    },
    checkEin() {
      // let ein = prompt("What is your ein?")
      this.$store.dispatch("getApiOrg", this.newOrg.EIN);
    }
  }
  //components: {  }
};
</script>

<style scoped>
img {
  max-width: 100px;
}
</style>
