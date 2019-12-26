<template>
 <div>
   <div class="topBar">
     <img src="../assets/logoImg.gif">
   </div>
   <div class="searchScreen">
     <div class="searchResultBar" style="margin-top: -16px;">
       <p>Market tracker</p>
     </div>
     <div class="searchScreenSection">
       <div>
           <label>Company:</label>
           <input type="text" v-model="companyName">
       </div>
       <div>
           <label style="margin-left: 45px;">Listing period:</label>
           <input class="periodDropDownTextBox" type="text" v-model="selectedValue" v-on:click="clickOnDroDown()">
           <div id="dropDown" class="periodDropDown">
             <div class="periodDropDownItem" v-on:click="selectValue('Last 1 year')">
               <div class="periodDropDownItemText">Last 1 year</div>
             </div>
             <div class="periodDropDownItem" v-on:click="selectValue('Last 2 year')">
               <div class="periodDropDownItemText">Last 2 year</div>
             </div>
             <div class="periodDropDownItem" v-on:click="selectValue('Last 5 year')">
               <div class="periodDropDownItemText">Last 5 year</div>
             </div>
             <div class="periodDropDownItem" v-on:click="selectValue('More than 5 year')">
               <div class="periodDropDownItemText">More than 5 year</div>
             </div>
           </div>
       </div>
     </div>
     <div class="searchButton">
       <button v-on:click="searchFunction()">Search</button>
     </div>
   </div>
   <div class="resultBody">
     <div class="searchResultBar fixedBar">
       <p>Market tracker result</p>
     </div>
     <div class="searchResultSection">
       <div class="searchResultBox">
         <div class="searchResultBar fixedBar resultSubHeading">
           <p>Company Information</p>
         </div>
         <div class="resultInside">
           <div id="info"></div>
         </div>
       </div>
       <div class="searchResultBox">
         <div class="searchResultBar fixedBar resultSubHeading">
           <p>Corporate Actions</p>
         </div>
         <div class="resultInside">
           <div id="corporateActions"></div>
         </div>
       </div>
       <div class="searchResultBox">
         <div class="searchResultBar fixedBar resultSubHeading">
           <p>Announcements</p>
         </div>
         <div class="resultInside">
           <div id="announcements"></div>
         </div>
       </div>
     </div>
   </div>
 </div>
</template>

<script>
import axios from 'axios'
// let data1
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      selectedValue: 'Select more than 5 years',
      companyName: 'Type INFY'
    }
  },
  methods: {
    clickOnDroDown: function () {
      document.getElementById('dropDown').style.display = 'block'
    },
    selectValue: function (value) {
      this.selectedValue = value
      document.getElementById('dropDown').style.display = 'none'
    },
    searchFunction: function () {
      if (this.selectedValue === 'More than 5 year' && this.companyName === 'INFY') {
        axios({
          'async': true,
          'crossDomain': true,
          'url': 'https://cors-anywhere.herokuapp.com/https://www1.nseindia.com/marketinfo/companyTracker/compInfo.jsp?symbol=INFY&series=EQ',
          'method': 'GET',
          'headers': {
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Methods': 'POST, GET, PUT, OPTIONS, DELETE',
            'Access-Control-Allow-Headers': 'Access-Control-Allow-Methods, Access-Control-Allow-Origin, Origin, Accept, Content-Type',
            'Content-Type': 'application/json',
            'Accept': 'application/json'
          }
        }).then(function (response) {
          let data1 = response.data
          document.getElementById('info').innerHTML = data1
        }, err => console.log('err1:', err))
        axios({
          'async': true,
          'crossDomain': true,
          'url': 'https://cors-anywhere.herokuapp.com/https://www1.nseindia.com/marketinfo/companyTracker/corpAction.jsp?symbol=INFY',
          'method': 'GET',
          'headers': {
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Methods': 'POST, GET, PUT, OPTIONS, DELETE',
            'Access-Control-Allow-Headers': 'Access-Control-Allow-Methods, Access-Control-Allow-Origin, Origin, Accept, Content-Type',
            'Content-Type': 'application/json',
            'Accept': 'application/json'
          }
        }).then(function (response) {
          let data2 = response.data
          document.getElementById('corporateActions').innerHTML = data2
        }, err => console.log('err2:', err))
        axios({
          'async': true,
          'crossDomain': true,
          'url': 'https://cors-anywhere.herokuapp.com/https://www1.nseindia.com/marketinfo/companyTracker/corpAnnounce.jsp?symbol=INFY',
          'method': 'GET',
          'headers': {
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Methods': 'POST, GET, PUT, OPTIONS, DELETE',
            'Access-Control-Allow-Headers': 'Access-Control-Allow-Methods, Access-Control-Allow-Origin, Origin, Accept, Content-Type',
            'Content-Type': 'application/json',
            'Accept': 'application/json'
          }
        }).then(function (response) {
          let data3 = response.data
          document.getElementById('announcements').innerHTML = data3
        }, err => console.log('err3:', err))
      } else {
        document.getElementById('info').innerHTML = document.getElementById('corporateActions').innerHTML = document.getElementById('announcements').innerHTML = 'Data not available'
        this.selectedValue = 'Select more than 5 years'
        this.companyName = 'Type INFY'
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.topBar{
  color: #888;
  position: fixed;
  top: 0px;
  background-color: white;
  width: 100%;
  text-align: left;
  box-shadow: -4px 0px 15px rgba(0, 0, 0, 0.2);
  z-index: 1;
}
.searchScreen{
  color: #888;
  position: fixed;
  top: 70px;
  width: 100%;
  height: 230px;
  background-color: rgba(0,0,0,0.05);
  text-align: left;
}
.resultBody{
  color: #888;
  /*background-color: rgba(212,235,242,0.3);*/
  background-color: rgba(0,0,0,0.05);
  position: fixed;
  top: 300px;
  width: 100%;
  height: calc(100vh - 300px);
  overflow-y: scroll;
  text-align: left;
}
.searchResultBar{
  background-color: white;
  box-shadow: -4px 0px 15px rgba(0, 0, 0, 0.2);
  z-index: 1;
  width: 100%;
  height: 30px;
  color: #3c3c3c;
  font-weight: 800;
  padding-left: 25px;
}
.searchResultSection{
  padding: 35px;
  display: flex;
  justify-content: space-evenly;
  /*background-color: rgba(0,0,0,0.05);*/
}
.searchScreenSection{
  padding: 15px 20px 20px 35px;
  display: flex;
  justify-content: space-around;
}
.fixedBar{
  position: fixed;
  line-height: 0;
}
.searchScreenSection input{
  border: 1px solid #cccccc;
  border-radius: 5px;
  padding: 7px;
  width: 400px;
  color: #3c3c3c;
  outline: none;
}
.searchScreenSection input:focus{
  border: 1px solid #1875f0;
}
.periodDropDown{
  position: absolute;
  z-index: 2;
  border-radius: 5px;
  background-color: white;
  color: #3C3C3C;
  font-size: 13px;
  width: 415px;
  margin-left: 150px;
  box-shadow: rgba(0, 0, 0, 0.5) 0px 0px 1px, rgba(0, 0, 0, 0.1) 0px 3px 10px;
}
.periodDropDownItem{
  padding: 11px 15px 11px 15px;
  cursor: pointer;
}
.periodDropDownItemText{

}
.periodDropDownItem:hover{
  color: #1875f0;
  background-color: #eee;
}
button{
  border-radius: 5px;
  border: 1px solid #1875f0;
  background-color: rgb(24, 117, 240);
  color: #ffffff;
  font-weight: 800;
  width: 170px;
  padding: 6px;
  transition: 0.4s ease;
  cursor: pointer;
  outline: none;
}
button:active{
  border: 1px solid #0835a0;
  background-color: #0835a0;
}
button:hover{
  box-shadow: 0 0.25em 0.75em rgba(0, 156, 255, .5);
}
.searchButton{
  text-align: center;
  margin-top: 35px;
}
#dropDown{
  display: none;
}
.searchResultBox{
  border-radius: 5px;
  background-color: white;
  width: 25%;
  padding: 15px;
  margin-top: 25px;
}
.resultSubHeading{
  width: calc(25% - 17px);
  margin-top: -15px;
  margin-left: -15px;
  border-radius: 5px;
  font-size: 14px;
  position: absolute;
  z-index: 0;
}
.resultInside{
  margin-top: 30px;
}
.periodDropDownTextBox{
  /*background-image: url(https://image.ibb.co/kRA2pq/expand-more-grey-24x24.png);*/
  background-image: url(../assets/downArrow.png);
  background-repeat: no-repeat;
  background-position: 385px 3px;
}
td{
  padding: 10px !important;
}
</style>
