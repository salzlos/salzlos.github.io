<template>
  <div
    id="salzlos"
    :class="{ colorized: isColorized, black: isBlack }"
    @click="clickNext()"
    @scroll.passive="clickNext()"
  >
    <SalzlosLogo v-if="viewIndex == 0" />
    <div id="salzlos-view-container">
      <img
        src="img/campaign/Selina_Salzlos_LowRes-11-.jpg"
        alt="campaign1"
        v-if="viewIndex == 1"
      />
      <img
        src="img/campaign/WOLKE716Kamp.Look2Ausschnitt.jpg"
        alt="campaign2"
        v-if="viewIndex == 2"
      />
      <SalzlosView v-if="viewIndex == 1" />
      <SalzlosView v-if="viewIndex == 2" />
    </div>
  </div>
</template>

<script>
import SalzlosView from './SalzlosView.vue';
import SalzlosLogo from './SalzlosLogo.vue';

export default {
  name: 'Salzlos',
  components: {
    SalzlosView,
    SalzlosLogo,
  },
  data: function() {
    return {
      viewIndex: 0,
      totalViews: 3,
      timeout: 1500,
      scrollEnabled: true,
    };
  },
  computed: {
    isColorized: function() {
      return this.viewIndex < 1;
    },
    isBlack: function() {
      return !this.isColorized;
    },
  },
  methods: {
    startShow: function() {
      this.nextView();
    },
    nextView: function() {
      if (++this.viewIndex == this.totalViews) {
        this.viewIndex = 0;
        this.$router.push({ path: 'shop' });
      } else {
        setTimeout(this.nextView, this.timeout);
      }
    },
    clickNext: function() {
      if (++this.viewIndex == this.totalViews) {
        this.viewIndex = 0;
        this.$router.push({ path: 'shop' });
      }
    },
    scrollNext: function() {
      if (this.scrollEnabled) {
        this.scrollEnabled = false;
        this.clickNext();
        window.setTimeout(
          (() => {
            this.scrollEnabled = true;
          }).bind(this),
          500
        );
      }
    },
  },
  mounted: function() {
    setTimeout(this.nextView, this.timeout);
  },
};
</script>

<style lang="sass" scoped>
#salzlos
  padding: 50px
  width: calc(100% - 100px)
  height: calc(100% - 100px)
#salzlos-view-container
  position: absolute
  top: 0px
  left: 0px
  bottom: 0px
  right: 0px
  display: flex
  flex-direction: row
  align-items: center
  justify-content: space-around
  img
    max-width: 80%
    max-height: 100%
.header
  font-size: 3em
  margin: 0
.colorized
  background-image: url("../assets/bg.jpg")
  background-repeat: no-repeat
  background-size: cover
  background-position: 50% 45%
.black
  background-color: #f1ddcf
  background-size: 100% 100%
.noselect
  -webkit-touch-callout: none
  -webkit-user-select: none
  -khtml-user-select: none
  -moz-user-select: none
  -ms-user-select: none
  user-select: none
.salzlos-logo
  position: absolute
  bottom: 50px
  left: 50px
  width: 570px
  height: 200px
@media only screen and (max-width: 1000px)
  .salzlos-logo
    left: 20px
    bottom: 20px
    width: 250px
    height: 80px
</style>
