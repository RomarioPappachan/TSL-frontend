
<template>
  <div>
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Document</title>
      <link rel="preconnect" href="https://fonts.googleapis.com" />
      <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />

      <link
        href="https://fonts.googleapis.com/css2?family=Crimson+Text:wght@400;600;700&family=Poppins:wght@100;300;400;600;700&family=Work+Sans:wght@100;200;400;500;600;800&display=swap"
        rel="stylesheet"
      />

       <!-- Bootstrap CDN CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous">

    </head>

    
    <div class="hero-main-container">
        

      <select class="home-language-select-button" v-model="selectedLanguage" @change="changeLanguage" @load="initial">
        <option value="" disabled selected>Audio language</option>
        <option v-for="(audio, language) in audios" :key="language" :value="language" style="background-color: #081E59;">
          {{ language }}
        </option>
      </select>
          
      <button class="proceed-button"  @click="toggleLogin">Proceed</button>         <!-- v-on:click="proceedClicked" -->
    




      <!-- Sliding Container -->
      

      <div :class="{ 'login-container': true, 'show-login': isLoginVisible }">
      <!-- <div v-bind:class = "[proceedClicked ? 'parent-container container-fluid m-0 p-0' : 'parent-container container-fluid m-0 p-0 hide']"> -->
     

        <div class="row g-0 m-0 p-0">

          <div class="col-md-4 slide-column-img">
          </div>

          <div class="col-md-8 m-0 p-0 columns slide-column-form-container">

            <!-- Progress Bar and Heading -->

            <div class="audio-section w-100">
              
              <div class="row w-100 h-100 d-flex justify-content-center align-items-center">
                <div class="col-8 col-md-10 h-100">
                  <AudioPlayer class="w-100" :selectedLanguage="selectedLanguage" :audios="audios"/>
                </div>
                <div class="col-4 col-md-2 h-100 d-flex justify-content-center align-items-center">
                  <select class="reg-language-select-button" v-model="selectedLanguage" @change="changeLanguage" @load="initial">
                    <option disabled value="">Select a language</option>
                    <option v-for="(audio, language) in audios" :key="language" :value="language">{{ language }}</option>
                  </select>
                </div>
              </div>
             

              

              
            </div>

            <div class="parent-heading">Satyam vada | Dharmam chara</div>


            <!-- Form parent container -->

            <div class="w-100 m-0 form-container-wrapper">
              <div class="row g-4 container-fluid form-parent-container">
                <div class="col-12">
                  
                  <div class="row gx-4">
                    <div class="col-md-6 gy-4 form-input-container">
                      <input type="text" class = "fname form-input-field w-100 h-100" placeholder = "First name" v-model="fname">
                      <!-- <span :class="[errors.fname ? 'show-error' : 'hide-error']">First name is empty</span> -->
                    </div>
                    <div class="col-md-6 gy-4  form-input-container">
                      <input type="text" class = "lname form-input-field w-100 h-100" placeholder = "Last name" v-model="lname">
                      <!-- <span :class="[errors.lname ? 'show-error' : 'hide-error']">Last name is empty</span> -->
                    </div>
                  </div>

                  <div class="row gx-4">
                    <div class="col-md-6 gy-4 form-input-container">
                      <input type="text" class = "email form-input-field w-100 h-100" placeholder = "Email" v-model="email">
                      <!-- <span :class="[errors.email ? 'show-error' : 'hide-error']">Email is empty</span> -->
                    </div>
                    <div class="col-md-6 gy-4 form-input-container">
                      <div class="row h-100">
                        <div class="col-8 h-100">
                          <!-- <input type="text" class = "dob form-input-field w-100 h-100" placeholder = "DOB"> -->
                          <VueDatePicker class="dob form-input-field w-100 h-100" v-on:change = "showDate" v-model="dob" v-bind:enable-time-picker="false" auto-apply placeholder="DOB" ></VueDatePicker>
                        </div>
                        <div class="col-4 h-100 d-flex">
                          <div class="h-100 d-flex justify-content-center align-items-center">
                            <div class="gender-wrapper w-50 h-100 d-flex flex-column justify-content-center align-items-center">
                              <img src = "./images/female.png" class = "w-50 mb-1"/>
                              <input class="gender-radio-button" type="radio" name="select" id="" value="female" v-model="gender"/>
                            </div>
                            <div class="gender-wrapper w-50 h-100 d-flex flex-column justify-content-center align-items-center">
                              <img src = "./images/male.png" class = "w-50 mb-1"/>
                              <input class="gender-radio-button" type="radio" name="select" id="" value="male" v-model="gender"/>
                            </div>
                          </div>
                        </div>
                      </div>
                      <!-- <span :class="[errors.dob ? 'show-error' : 'hide-error']">Select a dete of birth</span> -->
                      <!-- <span :class="[errors.gender ? 'show-error' : 'hide-error']">Select a gender</span> -->
                    </div>
                  </div>

                  <div class="row gx-4">
                    <div class="col-md-6 gy-4 form-input-container">
                      <select class="count form-input-field w-100 h-100" v-model="country">
                        <option disabled value="">Select a country</option>
                        <!-- Placeholder option -->
                        <option v-for="country in countries" :key="country.id" :value="country.name">{{ country.name }}</option>
                      </select>
                      <!-- <span :class="[errors.country ? 'show-error' : 'hide-error']">Select a Country</span> -->
                    </div>
                    <div class="col-md-6  gy-4 phone-code-n-number form-input-container">
                      <div class="row h-100 g-0 d-flex justify-content-between">

                        <div class="col-3 h-100 gx-0">
                          <div class="h-100 pe-3">
                            <div class="country-flag form-input-field w-100 h-100 d-flex justify-content-center align-items-center">
                              <img class="country-flag-image" v-bind:src="showFlag(country)"/>
                            </div>
                          </div>
                        </div>
                        <div class="col-2 h-100 gx-0">
                          <div class="country-code form-input-field w-100 h-100 d-flex justify-content-center align-items-center">{{ country_code }}
                        </div>
                      </div>
                      <div class="col-7 h-100 gx-0">
                        <input type="text" class = "phone-number form-input-field w-100 h-100" v-model="phone">
                      </div>
                    </div>
                    <!-- <span :class="[errors.gender ? 'show-error' : 'hide-error']">Enter a Phone number</span> -->
                  </div>
                </div>
        
                  <div class="row gx-4">
                    <div class="col-md-6 gy-4 form-input-container">
                             
                      <div class="form-input-field w-100 h-100 form-input-field d-flex justify-content-around">
                        <div class="search-icon h-100 d-flex flex-column justify-content-center align-items-center">🔍</div>

                        <div class="d-flex flex-column justify-content-center align-items-center">Social media
                          <input class="reference-radio-button" style="background: none" type="radio" v-model="reference" name="source" value="social_media"/>
                        </div>

                        <div class="d-flex flex-column justify-content-center align-items-center">Reference
                          <input class="reference-radio-button" style="background: none" type="radio" v-model="reference" name="source" value="reference"/>
                        </div>

                        <div class="d-flex flex-column justify-content-center align-items-center">News
                          <input class="reference-radio-button" style="background: none" type="radio" v-model="reference" name="source" value="news"/>
                        </div>
                      </div>
                      <!-- <span :class="[errors.reference ? 'show-error' : 'hide-error']">Please select an option</span> -->
                    </div>

                    <div class="col-md-6 gy-4 form-input-container">

                      <VueMultiselect 
                        class = "language form-input-field w-100 h-100"
                        v-model="value" 
                        tag-placeholder="Add this as new tag" 
                        placeholder="Select Languages" 
                        label="name" 
                        track-by="code" 
                        :options="options" 
                        :multiple="true" 
                        :taggable="true" 
                        @tag="addTag" 
                        v-bind:searchable = "false"
                      ></VueMultiselect>
                      <!-- <span :class="[errors.value ? 'show-error' : 'hide-error']">Please select one or more languages</span> -->
                    </div>
                  </div>
                </div>
        
                <div class="col-12 form-input-container">
                  <div class="row h-100">
                    <div class="col-12">
                      <!-- <input type="text" class = "special_remarks form-input-field w-100 h-100" placeholder = "Special remarks"> -->
                      <input type="text" class = "form-input-field w-100 h-100" placeholder="Special remarks" v-model="special_remarks" v-on:change="specialCount" maxlength="500"/>
                    </div>
                  </div>
                </div>
                <!-- <span :class="[errors.special_remarks ? 'show-error' : 'hide-error']">Please enter your remarks</span> -->
                
                <div class="col-12 g-0 text-end"><span class="remarks-count">{{ 500 - special_remarks_count }}/500</span></div>
 
                <div class="col-12 form-input-container">
                  <div class="row h-100">
                    <div class="col-12">
                      <!-- <input class = "submit form-input-field w-100 h-100" type="submit" value ="Submit"> -->
                      <input v-on:click="register" class = "submit form-input-field w-100 h-100" type="submit" value="Submit"/>
                    </div>
                  </div>
                </div>
              </div>

            </div>

        
            <!-- Registration sliding page Footer -->

            <div class="footer-container-wrapper w-100">
              <div class="footer row">
                <div class="footer-sub-grp col-3">
                  <span class="footer-update">39997</span>
                  <span class="footer-head">Total meditators</span>
                </div>
                <div class="footer-sub-grp col-3">
                  <span class="footer-update"> 1136 </span>
                  <span class="footer-head">Waiting List</span>
                </div>
                <div class="footer-sub-grp col-3">
                  <span class="footer-update">39850</span>
                  <span class="footer-head">Benefactories</span>
                </div>
                <div class="footer-sub-grp col-3">
                  <span class="footer-update">1648</span>
                  <span class="footer-head">Classes</span>
                </div>
              </div>
            </div>
          </div>

        </div>
      </div>













      <!-- --------------------------Confirmation Popup------------------- -->


      <div v-bind:class="[toggle_submit ? 'pop' : 'pop hide']">
        <div class="pop-head">Confirm Email & Phone Number ?</div>
        <div class="pop-content">
          <span class="message"> {{ phone }} & {{ email }}</span>
          <span class="prompt">
            Would you like to edit the Email & PhoneNumber ?
          </span>
          <div class="pop-btn">
            <button class="ok" v-on:click="submitToExpress">OK</button>

            <button class="edit" v-on:click="editpress">Edit</button>
          </div>
        </div>
      </div>





      <!-- User already exist Popup -->

      <div v-bind:class="[close_btn ? 'pop' : 'pop hide']">
        <div class="pop-head">Confirm Email & Phone Number ?</div>
        <div class="pop-content">
          <span class="message">User already exists</span>

          <div
            class="pop-btn"
            style="width: 100%; display: flex; justify-content: center"
          >
            <button class="ok" v-on:click="closeExist">Ok</button>
          </div>
        </div>
      </div>





      <!-- otp -->
      <div v-bind:class="[show_otp_popup ? 'otp' : 'otp hide']">
        <div class="otp-head">Enter otp</div>

        <div class="otp-content">
          <div class="otp-input-grp">
            <!-- <input v-model="otpInput1"  maxlength="1" v-on:input="focusNext(1)" id='otp-input' type="text">
                      <input  v-model="otpInput2" type="text" maxlength="1" v-on:input="focusNext(2)" id='otp-input'>
                      <input  v-model="otpInput3" type="text" maxlength="1" v-on:input="focusNext(3)" id='otp-input'>
                        <input v-model="otpInput4" type="text" maxlength="1" id='otp-input'> -->
            <input
              v-model="otpInput1"
              maxlength="1"
              v-on:input="focusNext(1, $event)"
              id="otp-input"
              type="text"
            />
            <input
              v-model="otpInput2"
              maxlength="1"
              v-on:input="focusNext(2, $event)"
              id="otp-input"
              type="text"
            />
            <input
              v-model="otpInput3"
              maxlength="1"
              v-on:input="focusNext(3, $event)"
              id="otp-input"
              type="text"
            />
            <input
              v-model="otpInput4"
              maxlength="1"
              id="otp-input"
              type="text"
            />
          </div>
          <div class="otp-timer">
            {{ message }}
          </div>

          <div class="otp-btn-grp">
            <button class="otp-submit" v-on:click="resendOtp">Resend</button
            ><button class="resend" v-on:click="submitOtp">Submit</button>
          </div>
        </div>
      </div>





      <!-- show success card -->
      
      <div
        v-bind:class="[show_registration_success ? 'overlay' : 'overlay hide']"
      >
        <div class="registration-card">
          <div class="card-div-top">
            <div class="card-number">
              <p>card number</p>
              <h1>10040</h1>
            </div>
            <div class="card-logo-container">
              <img
                class="card-logo"
                src="../components/logo.png"
                alt="Thasmai logo"
              />
            </div>
          </div>

          <div class="card-div-middle">
            <img class="chip" src="../components/chip.png" alt="chip" />
            <h3>Registration Successful</h3>
            <button>OK</button>
          </div>

          <div class="card-div-bottom">
            <div class="cardholder-group">
              <div class="cardholder-name">
                <p>{Cardholder Name}</p>
                <h2>{{ this.fname }}{{ this.lname }}</h2>
              </div>
              <div class="cardholder-img-container">
                <img
                  class="cardholder-img"
                  src="../components/user.png"
                  alt="User logo"
                />
              </div>
            </div>

            <div class="validity">
              <p>VALID THRU</p>
              <p>11/27</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import axios from "axios";
import VueDatePicker from "@vuepic/vue-datepicker";
import "@vuepic/vue-datepicker/dist/main.css";
import VueMultiselect from 'vue-multiselect'
import "bootstrap";
import AudioPlayer from "./AudioPlayer.vue";
import VueSocketIO from 'vue-socket.io';
export default {
  name: "RegUser",
  components: { VueDatePicker, AudioPlayer,VueMultiselect},

  data() {
  
    return {
      // audiolanguage : "https://dl.sndup.net/kr6x/TSL_ENGLISH.mp4",
      value: [
          // { name: 'Javascript', code: 'js' }
        ],
        options: [
          { name: 'English', code: 'English' },
          { name: 'Malayalam', code: 'Malayalam' },
          { name: 'Kannada', code: 'Kannada' },
          { name: 'Tamil', code: 'Tamil' },
          { name: 'Telugu', code: 'Telugu' }
        ],
      special_remarks_count: 0,
      proceedclicked: false,
      selectedLanguage: "",
      message: "1:30",
      show_registration_success: false,
      show_otp_popup: false,
      close_btn: false,
      toggle_submit: false,
      audios: {
        english: "https://dl.sndup.net/kr6x/TSL_ENGLISH.mp4",
        malayalam: "https://dl.sndup.net/cr76/TSL_Malayalam.mp4",
        hindi: "https://dl.sndup.net/rrqr/TSL_Hindi.mp4",
        kannada: "https://dl.sndup.net/jrr7/TSL_Kannada.mp4",
        tamil: "https://dl.sndup.net/vtdn/TSL_Tamil.mp4",
        telugu: "https://dl.sndup.net/cxfj/TSL_Telugu.mp4",
      },
      otpInput1: "",
      otpInput2: "",
      otpInput3: "",
      otpInput4: "",
      otp: "",
      countries: [],
      country_code: "",
      errors: {},
      fname: "",
      lname: "",
      gender: "",
      email: "",
      dob: "",
      country: "India",
      phone: "",
      reference: "",
      languages: "",
      special_remarks: "",


      isLoginVisible: false,
      isRedBackground: false,
      popupVisible: false
    };
  },
  watch: {
    special_remarks(newVal) {
      // Update the character count whenever 'special_remarks' changes
      this.special_remarks_count = newVal.length;
    },
  },
  created() {
    try {
      axios
        .get("http://89.47.164.122:5000/api/registrations/countrieslist")
        .then((res) => {
          console.log(res.data);
          this.countries = res.data;
        });
    } catch (err) {
      console.log(err);
    }
  },

  methods: {
    showDate(){console.log(this.dob,'dobshow')},
    addTag(newTag) {
      const tag = {
        name: newTag,
        code: newTag.substring(0, 2) + Math.floor(Math.random() * 10000000),
      };
      this.options.push(tag);
      this.value.push(tag);
    },

    toggleLogin() {
      this.isLoginVisible = !this.isLoginVisible;
      this.isRedBackground = !this.isRedBackground;
    },


    proceedClicked() {
      this.proceedclicked = true;
    },
    register() {
      // validaton goes here
      this.errors = {};
      if (this.fname === "") {
        this.errors.fname = "fname";
      }
      this.toggle_submit = true;

      console.log(
        this.fname,
        this.lname,
        this.reference,
        this.phone,
        this.gender
      );
    },

    editpress() {
      this.toggle_submit = false;
    },
    focusNext(index, event) {
      const value = event.target.value;
      if (value.length === 1 && index < 4) {
        const nextInput = this.$refs[`otp-input-${index + 1}`];
        if (nextInput) {
          // Use $nextTick to ensure the next input is fully rendered before focusing
          this.$nextTick(() => {
            nextInput.focus();
          });
        }
      }
    },
    submitToExpress() {
      console.log('submit')
      this.toggle_submit = false;
      axios
        .post("http://192.168.1.72:3000/api/registrations/registerUser", {
          // first_name: this.fname,
          // last_name: this.lname,
          email: this.email,
          phone: this.phone,
          // DOB: this.dob,
          // gender: this.gender,
          // country: this.country,
          // reference: this.reference,
          // languages: this.language,
          // remark: this.special_remarks,
        })
        .then((res) => {
          console.log(res.status);
          if (res.status === 200) {
            this.show_otp_popup = true;
          }
        })
        .catch((err) => {
          console.log(err.response.status);
          if (err.response.status) {
            this.close_btn = true;
          }
        });
    },
    submitOtp() {
    
      this.otp =
        this.otpInput1 + this.otpInput2 + this.otpInput3 + this.otpInput4;
      console.log(this.dob, "dob");
      this.dob = this.dob.split(",")[0]
      console.log(this.dob)

      axios
        .post("http://192.168.1.72:3000/api/registrations/verify_otp", {
          OTP: this.otp,
          phone: this.phone,
          first_name: this.fname,
          last_name: this.lname,
           DOB: this.dob,
          gender: this.gender,
          country: this.country,
          reference: this.reference,
          languages: this.language,
          remark: this.special_remarks,
        })
        .then((res) => {
          console.log(res);

          if (res.status === 200) {
            this.show_otp_popup = false;
            this.show_registration_success = true;
          }
          else{
            this.message = "Invalid otp";
          }
        })
        .catch((err) => {
          if (err.response.status === 400) {
            this.message = "Invalid otp";
          }
        });
    },
    resendOtp() {
      console.log("resend");

      this.show_otp_popup = false;
      this.otpInput1 = "";
      this.otpInput2 = "";
      this.otpInput3 = "";
      this.otpInput4 = "";

      this.show_otp_popup = true;

      this.toggle_submit = false;
      axios
        .post("http://192.168.1.72:3000/api/reistrations/resendOtp", {
          // first_name: this.fname,
          // last_name: this.lname,
          // email: this.email,
          phone: this.phone,
          // DOB: this.dob,
          // gender: this.gender,
          // country: this.country,
          // reference: this.reference,
          // languages: this.language,
          // remark: this.special_remarks,
        })
        .then((res) => {
          console.log(res.status);
          if (res.status === 200) {
            this.show_otp_popup = true;
          }
        })
        .catch((err) => {
          console.log(err.response.status);
          if (err.response.status) {
            this.close_btn = true;
          }
        });
    },
    changeLanguage() {
      // Change the audio source when a different language is selected
      console.log(this.selectedLanguage); // Log the selected language (optional)
      this.audiolanguage = this.audios[this.selectedLanguage];
    },
    changeDate() {
      this.dob = this.dob.split(",")[0].split("T")[0];   
    },
    closeExist() {
      this.close_btn = false;
    },
    initial() {
      this.selectedLanguage = "english";
    },
    showFlag(country_name) {
      let country = this.countries.find((value) =>
        value.name.startsWith(country_name)
      );

      if (country && country.phonecode) {
        this.country_code = country.phonecode;
        return country.flag;
      } else {
        // Handle cases where the country or phonecode is undefined
        return ""; // Return a default value or handle the situation accordingly
      }
    },
  },
};
</script>

<style src="vue-multiselect/dist/vue-multiselect.css"></style>

<style scoped >

@import "./reg.css";

</style>
