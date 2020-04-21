<template>
  <div id="conf-app">
    <div class="conf-app" :class="{'conf-app--active' : appLaunched }">
      <img alt="Vue logo" src="./assets/logo.png">
      <HelloWorld :msg="`Here you go! :)`" />
    </div>
    <button class="launch-conf-app" data="{site: 'Mayfair', floor: 1}">Go Configure</button>

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

          // fake loading to show brand name
          console.log("Loading...");

          // launch app after 1 second
          setTimeout(() => {
            this.launchData = btn.target.getAttribute('data');
            this.launchApp();
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
