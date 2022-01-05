<template>
  <main>
    <div class="page-container">
        <div class="input-container">
            <h1 data-highlightword="FAKE ">NEWS DETECTOR</h1>
            <span>Insert news to check:</span>
            <br>
            <br>
            <span class="textarea">
                <textarea v-model="message" placeholder="add multiple lines" rows="15" cols="80"></textarea>
            </span>
            <br>
            <button v-on:click="checkText">Check</button>
        </div>
    </div>
  </main>
</template>

<script>

import Swal from 'sweetalert2/dist/sweetalert2.js'

import 'sweetalert2/src/sweetalert2.scss'

import axios from 'axios'

export default {
  methods: {
    checkText () {
      var bodyFormData = new FormData();
      bodyFormData.append('text', this.message);

      axios({
        method: "post",
        url: "https://ccsfakeapi.azurewebsites.net/check",
        data: bodyFormData,
        headers: { "Content-Type": "multipart/form-data" },
      }).then(response => {
        this.handleCheck(response.data)
      })
    },
    handleCheck (data) {
      let popupContent;
      if(data.response == 'Fake') {
        popupContent = '<p>' + this.message + '</p>' + '<p style="color:red;font-size:30px;"><strong>FALSE</strong></p>';
      } else {
        popupContent = '<p>' + this.message + '</p>' + '<p style="color:green;font-size:30px;"><strong>TRUE</strong></p>';
      }
      Swal.fire({
        title: 'RESULTS',
        html: popupContent,
        width: 1000,
        padding: '3em',
        color: '#ffffff',
        background:  '#2e2e2e',
        confirmButtonColor: "#1beabd"
      })
    }
  }
}
</script>

<style>
html {
    width: 100%;
    min-height: 100%;
    overflow: auto;
}


body {
    width: 100%;
    min-height: 100vh;
    overflow: auto;
    font-family: "Avant Garde", Avantgarde, "Century Gothic", CenturyGothic, "AppleGothic", sans-serif; 
}

#app {
    font-family: "Avant Garde", Avantgarde, "Century Gothic", CenturyGothic, "AppleGothic", sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #FDF5E6;
    letter-spacing: .05em;
    text-shadow: 
      0 -1px 0 #fff, 
      1px 1px 0 #2e2e2e, 
      2px 2px 0 #2c2c2c, 
      3px 3px 0 #2a2a2a, 
      4px 4px 0 #282828, 
      5px 5px 0 #262626, 
      6px 6px 0 #242424, 
      7px 7px 0 #222, 
      8px 8px 0 #202020, 
      0 22px 30px rgba(0, 0, 0, 0.9);
    background-color: #2e2e2e;
    width: 100%;
    min-height: 100vh;
}

.page-container {
  display: flex;
  width: 100%;
  height: 100%;
  justify-content: center;
}
h1[data-highlightword] {
    font-family: "Avant Garde", Avantgarde, "Century Gothic", CenturyGothic, "AppleGothic", sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #FDF5E6;
    margin-top: 20px;
    letter-spacing: .005em;
    text-shadow:
        1px 1px 0 #2e2e2e,
        2px 2px 0 #2c2c2c,
        3px 3px 0 #2a2a2a,
        4px 4px 0 #282828,
        5px 5px 0 #262626,
        6px 6px 0 #242424,
        7px 7px 0 #222,
        8px 8px 0 #202020,
        0 22px 30px rgba(0, 0, 0, 0.9);
}

h1[data-highlightword]::before {
    content: attr(data-highlightword);
    color: #b30000;

}

button {
    color: #fff;
    justify-content: center;
    align-items: center;
    padding: 0 20px;
    padding-top: 0px;
    padding-right: 20px;
    padding-bottom: 0px;
    padding-left: 20px;
    min-width: 160px;
    height: 62px;
    background-color: #1beabd;
    text-decoration: none;
    margin: 4px 2px;
    cursor: pointer;
    font-size: 16px;
    line-height: 1.2;
    text-transform: uppercase;
    -webkit-transition: all 0.4s;
    -o-transition: all 0.4s;
    -moz-transition: all 0.4s;
    transition: all 0.4s;
    z-index: 1;
    position: relative;
    border-width: 8px;
    border-color: #1beabd;
}

textarea {
    position: relative;
    font-size: 10px;
    color: white;
    background: #404040;
    padding: 15px;
    border-width: 4px;
    border-color: #1beabd;
}

::placeholder {
    color: #f2f2f2;
    font-size: 14px;
}

.input-container {
    font-family: "Avant Garde", Avantgarde, "Century Gothic", CenturyGothic, "AppleGothic", sans-serif;
    font-size: 40px;
    text-align: center;
    text-transform: uppercase;
    text-rendering: optimizeLegibility;
    background-color: #696969;
    padding: 20px;
    text-shadow:
        0 -1px 0 #fff,
        1px 1px 0 #2e2e2e,
        2px 2px 0 #2c2c2c,
        3px 3px 0 #2a2a2a,
        4px 4px 0 #282828,
        5px 5px 0 #262626,
        0 22px 30px rgba(0, 0, 0, 0.9);
}

.popup {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 99;
  background-color: rgba(0,0,0,0.2);
  display: flex;
  align-items: center;
  justify-content: center;
}

.popup-inner {
  background: #FFF;
  padding: 32px;
}

</style>
