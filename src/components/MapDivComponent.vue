<template>
  <div class="mapDiv">
    <div id="map" @click="setLocation">
      <div id="dots">
        <div v-bind:style="{ left: location.x + 'px',
                                top: location.y + 'px'}"
             v-bind:key="'dots'">
          T </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "MapDivComponent",
  data:function () {
    return {
      location: {
        x: 0,
        y: 0
      }
    }
  },
  methods: {
    setLocation: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top};
      this.location = {x: event.clientX - 10 - offset.x,
        y: event.clientY - 10 - offset.y}
      this.$emit('setLocation', {location: this.location})
    },
  }
}

</script>

<style>
.mapDiv {
  overflow: scroll;
}
#dots {
  position: relative;
  margin: 0;
  padding: 0;
  background-repeat: no-repeat;
  width:1920px;
  height: 1078px;
  cursor: crosshair;
}

#dots div {
  position: absolute;
  background: black;
  color: white;
  border-radius: 10px;
  width:20px;
  height:20px;
  text-align: center;
}
#map {
  background: url("../../public/img/polacks.jpg");
  height: 1078px;
  width: 1920px;
}
</style>