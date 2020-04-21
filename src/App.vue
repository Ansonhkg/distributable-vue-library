<template>
  <div id="conf-app">
    <div class="conf-app" :class="{'conf-app--active' : appLaunched }">

      <!-- fake loading -->
      <div class="conf-app__loading" :class="{'conf-app__loading--false' : !launchLoading}">
        <img width="30px;" src="./assets/loading.svg"/>
      </div>
      
      <!-- result -->
      <div class="conf-app__result" :class="{'conf-app__result--active' : !launchLoading}">
        <img alt="Vue logo" src="./assets/logo.png">
        <HelloWorld :msg="`Here you go! :)`" />
      </div>
    </div>

    <!-- launch buttons -->
    <!-- <button class="launch-conf-app" data="{site: 'siteFoo', floor: 1}">Launch App</button><br>
    <button class="launch-conf-app" data="{site: 'siteBar', floor: 2}">Launch App 2</button><br>
    <button class="launch-conf-app" data="{site: 'siteHakuna', floor: 3}">Launch App 3</button><br> -->

    <!-- errors -->
    <div class="conf-error" :class="{'conf-error--active': errors.length > 0}">
      <div class="conf-error-title">Oops.. there seems to be some errors...</div>
      <ul v-for="(err, idx) in errors" :key="idx">
        <li>{{ err.type }}:: {{ err.message }}</li>
      </ul>
    </div>

  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  data(){
    return {
      appLaunched: false,
      launchLoading: false,
      launchData: {},
      // errors
      errors:[]
    }
  },
  components: {
    HelloWorld
  },
  methods:{
    /**
     * Launch app by toggling appLaunch variable
     * @return { void }
     */
    launchApp(){
      this.appLaunched = true
    },

    /**
     * Mount a launch button to class 'launch-conf-app'
     * Show error message if it doesn't exist
     * @return { void }
     */
    mountLaunchTrigger(){
      var btnsLaunchApp = document.getElementsByClassName('launch-conf-app');
      
      // if doesn't exists
      if(btnsLaunchApp.length <= 0){
        this.errors.push({
          type: 'LaunchError',
          message: 'Cannot find class .launch-conf-app',
        });
        return;
      }

      // add event listeners to .launch-conf-app buttons
      [...btnsLaunchApp].forEach((btn) => {
        btn.addEventListener('click', (btn) => {
          
          this.launchApp();

          // fake loading to show brand name
          this.launchLoading = true;
          console.log("Loading...");

          // show content after 1 second
          setTimeout(() => {
            this.launchLoading = false;
            this.launchData = btn.target.getAttribute('data');

          }, 1000);
        })
      })
    }
  },
  mounted(){
    this.mountLaunchTrigger();
  }
}
</script>

<style>
#conf-app{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

/** ===== app ===== */
.conf-app{
  text-align: center;
  position: fixed;
  padding-top: 60px;
  top: 0;
  left: 0;
  background: rgba(0,0,0,0.5);
  width: 100%;
  height: 100%;
  transition: all linear 0.3s;
  opacity: 0;
  pointer-events: none;
}
.conf-app--active{
  opacity: 1 !important;
  pointer-events: unset;
}
.conf-app__loading{
  width: 100%;
  height: 100%;
  display: flex;
  position: fixed;
  top:0;
  left: 0;
  transition: 0.3s linear all;
  opacity: 1;
}
.conf-app__loading > img{
  margin: auto;
}
.conf-app__loading--false{
  opacity: 0;
  pointer-events: none;
}
.conf-app__result{
  visibility: none;
  opacity: 0;
  transform: translateY(10px);
}
.conf-app__result--active{
  opacity: 1;
  transition: 0.5s linear all;
  transform: translateY(0);
}

/** ===== errors ===== */
.conf-error{
  position: fixed;
  bottom: 0;
  width: 100%;
  min-height: 30px;
  background: rgba(255, 188, 188, 0.5);
  left: 0;
  font-size: 13px;
  border: 1px solid #efacb8;
  transition: 0.3s all linear;
  opacity: 0;
  visibility: hidden;
  pointer-event: none;
}
.conf-error--active{
  pointer-event: unset;
  opacity: 1;
  visibility: visible;
}
.conf-error-title{
  margin-left: 5px;
  margin-top: 5px;
  font-weight: bold;
}
</style>
