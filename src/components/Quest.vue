<template>
<div id="quest">
  <div id="map">
    <div class="navBar">
        <svg width="20" height="28" class="backButton" viewBox="0 0 20 28" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M15.4393 12.9393L6.99998 4.5C6.4477 3.94771 5.55227 3.94771 4.99998 4.5C4.4477 5.05228 4.4477 5.94771 4.99998 6.5L12.5 14L4.99998 21.5C4.4477 22.0523 4.4477 22.9477 4.99998 23.5C5.55227 24.0523 6.4477 24.0523 6.99998 23.5L15.4393 15.0607C16.0251 14.4749 16.0251 13.5251 15.4393 12.9393Z" fill="#3F8AE0"/>
        </svg>
      <img class="infoBtn" @click="showPopup" src="../assets/questBtn.svg" alt="info">
    </div>

    <div class="popupHint">
      <div class="close" @click="closePopup">&times;</div>

      <b-col cols="12" class="mt-3">
        <p class="primaryText">
          Медный всадник
        </p>

        <label for="tasks">Описание задач</label>
        <div id="tasks" class="tasks">

          <b-button class="tag mb-2 activeTag">
            IT
          </b-button>

          <b-button class="tag mb-2 activeTag">
            Дизайн
          </b-button>
        </div>

        <p class="description mt-4 mb-5">Создайте свой первый чекпоинт, вы можете задать интересный вопрос или оставить послание игроку.</p>

        <div class="info pb-4 border-bottom">
          <b-row>
            <b-col cols="4">
              <div class="number">111</div>
              <div class="description">
                метров до цели
              </div>
            </b-col>
            <b-col cols="4">
              <div class="number">111</div>
              <div class="description">
                осталось чекпоинтов
              </div>
            </b-col>
            <b-col cols="4">
              <div class="number">111</div>
              <div class="description">
                пройдено чекпоинтов
              </div>
            </b-col>
          </b-row>
        </div>

        <b-button variant="link" class="btn-block text-decoration-none logOut"><router-link to="/">Выйти из квеста</router-link></b-button>
      </b-col>
    </div>

    <div class="popupHint2 popupHint">
      <div class="close" @click="closePopup2">&times;</div>

      <b-col cols="12" class="mt-3" style="height: 250px;">
        <p class="primaryText">
          {{ bestPlaces[id].title || 'Медный всадник' }}
        </p>

        <p class="primaryTextS">
          {{ bestPlaces[id].desc || 'Медный всадник, символ Санкт-Петербурга, на самом деле изготовлен не из меди, а из бронзы. Монумент был открыт в 1782 году по велению императрицы Екатерины Второй. В тот год отмечался 100-летний юбилей вступления на престол юного Петра.' }}
        </p>

        <div class="liker">

          <b-button variant="link" class="like" @click="rated = true">+</b-button>
          <b-button variant="link" class="like border-right-0" @click="rated = true">-</b-button>

        </div>
        <p class="description mt-1" v-if="rated">Спасибо за оценку</p>
      </b-col>

      <b-button variant="primary" class="primary position-relative" @click="newRoute">Подтвердить геолокацию</b-button>
    </div>
    <div id="mapContainer" class="w-100 h-100" ref="hereMap"></div>
  </div>
</div>
</template>

<script>
import axios from 'axios';

export default {
  name: "Quest",
  data() {
    return {
      platform: null,
      app_id: 'khnsdv2IWZS2FuTdJCbH',
      apikey: "kXJLOsUqIDBiL9E3YeHpDqVOX2WOENM2yOAkzd-yq78",
      center: { lat: 40.730610, lng: -73.935242 },
      userPosition: {},
      tmp: null,
      bestPlaces: ['test'],
      id: 0,
      rated: false
    };
  },
  async mounted() {
    // Initialize the platform object:
    const platform = new window.H.service.Platform({
      apikey: this.apikey
    });
    this.platform = platform;

    this.initializeHereMap();

    navigator.geolocation.getCurrentPosition(this.setCenter);

    this.showPopup2();

    axios
      .get("http://localhost:3000/bestPlaces")
      .then(response => {
        this.bestPlaces = response.data;
        if ( window.location.hash.includes("?") ) {
          this.id = window.location.hash.substr(window.location.hash.indexOf('=') + 1);
          console.log("id ", this.id);
        }
      });
  },
  methods: {
    initializeHereMap() {
      // rendering map
      const mapContainer = this.$refs.hereMap;
      const H = window.H;
      // Obtain the default map types from the platform object
      let maptypes = this.platform.createDefaultLayers();

      // Instantiate (and display) a map object:
      let map = new H.Map(mapContainer, maptypes.vector.normal.map, {
        zoom: 10,
        center: this.center
      });

      addEventListener("resize", () => map.getViewPort().resize());

      // add behavior control
      new H.mapevents.Behavior(new H.mapevents.MapEvents(map));

      // add UI
      H.ui.UI.createDefault(map, maptypes, 'ru-RU');
      // End rendering the initial map

      this.map = map;

      console.log(map);
    },
    setCenter({coords: {latitude, longitude}}) {
      const H = window.H;

      let coords = {lat: latitude, lng: longitude};

      this.userPosition = coords;
      this.map.setCenter(coords);

      let svgMarkup = '<svg width="28" height="48" viewBox="0 0 14 24" fill="none" xmlns="http://www.w3.org/2000/svg"><rect x="6" y="13" width="2" height="11" fill="url(#paint0_linear)"/> <circle cx="7" cy="7" r="7" fill="url(#paint1_radial)"/> <defs> <linearGradient id="paint0_linear" x1="7" y1="13" x2="7" y2="24" gradientUnits="userSpaceOnUse"> <stop stop-color="#5AA9FF"/> <stop offset="0.341281" stop-color="#B5D8FF"/> <stop offset="1" stop-color="white"/> </linearGradient><radialGradient id="paint1_radial" cx="0" cy="0" r="1" gradientUnits="userSpaceOnUse" gradientTransform="translate(7.875 5.25) rotate(95.7106) scale(8.79364 9.53555)"><stop stop-color="#BBDCFF"/> <stop offset="0.537828" stop-color="#208BFF"/> </radialGradient></defs> </svg>';

      // Create an icon, an object holding the latitude and longitude, and a marker:
      let icon = new H.map.Icon(svgMarkup),
        marker = new H.map.Marker(coords, {icon: icon});

      // Add the marker to the map and center the map at the location of the marker:
      this.map.addObject(marker);

      this.createRoute();
    },
    createRoute(latOffset = 0.1, lngOffset = 0.05) {
      const H = window.H;

      // Create the parameters for the routing request:
      let routingParameters = {
        'routingMode': 'fast',
        'transportMode': 'pedestrian',
        // The start point of the route:
        'origin': `${this.userPosition.lat},${this.userPosition.lng}`,
        // The end point of the route:
        'destination': `${this.userPosition.lat + latOffset},${this.userPosition.lng + lngOffset}`,
        // Include the route shape in the response
        'return': 'polyline',
        'apikey': 'kycyxKwH1RbOQGKq2zUMfYls5T6mOzUXsTVAoCKYvLg'
      };

      // Define a callback function to process the routing response:
      let onResult = (result) => {
        // ensure that at least one route was found
        if (result.routes.length) {
          result.routes[0].sections.forEach((section) => {
            // Create a linestring to use as a point source for the route line
            let linestring = H.geo.LineString.fromFlexiblePolyline(section.polyline);

            // Create a polyline to display the route:
            let routeLine = new H.map.Polyline(linestring, {
              style: { strokeColor: 'blue', lineWidth: 3 }
            });

            // Create a marker for the start point:
            // let startMarker = new H.map.Marker(section.departure.place.location);

            // Create a marker for the end point:
            // let endMarker = new H.map.Marker(section.arrival.place.location);
            let svgMarkup = '<svg width="28" height="48" viewBox="0 0 14 24" fill="none" xmlns="http://www.w3.org/2000/svg">\n' +
              '<rect x="6" y="13" width="2" height="11" fill="url(#paint0_linear)"/>\n' +
              '<circle cx="7" cy="7" r="7" fill="url(#paint1_radial)"/>\n' +
              '<defs>\n' +
              '<linearGradient id="paint0_linear" x1="6" y1="17.95" x2="8" y2="17.95" gradientUnits="userSpaceOnUse">\n' +
              '<stop stop-color="#A19B93"/>\n' +
              '<stop offset="0.261719" stop-color="#6B6763"/>\n' +
              '<stop offset="0.390625" stop-color="#AB9A8F"/>\n' +
              '<stop offset="0.574219" stop-color="#5D524F"/>\n' +
              '<stop offset="0.78125" stop-color="#655B59"/>\n' +
              '<stop offset="1" stop-color="#DEC9BC"/>\n' +
              '</linearGradient>\n' +
              '<radialGradient id="paint1_radial" cx="0" cy="0" r="1" gradientUnits="userSpaceOnUse" gradientTransform="translate(7.875 5.25) rotate(95.7106) scale(8.79364 9.53555)">\n' +
              '<stop stop-color="#FFA8A6"/>\n' +
              '<stop offset="0.537828" stop-color="#ED5A5A"/>\n' +
              '</radialGradient>\n' +
              '</defs>\n' +
              '</svg>\n';

            let icon = new H.map.Icon(svgMarkup);
            let endMarker = new H.map.Marker(section.arrival.place.location, {icon: icon});

            if (this.tmp) {
              this.map.removeObjects(this.tmp);
            }
            // Add the route polyline and the two markers to the map:
            this.tmp = [routeLine, endMarker];
            this.map.addObjects([routeLine, endMarker]);

            // Set the map's viewport to make the whole route visible:
            this.map.getViewModel().setLookAtData({bounds: routeLine.getBoundingBox()});
            this.map.setZoom(11);
          });
        }
      };

      // Get an instance of the routing service version 8:
      let router = this.platform.getRoutingService(null, 8);

      // Call calculateRoute() with the routing parameters,
      // the callback and an error callback function (called if a
      // communication error occurs):
      router.calculateRoute(routingParameters, onResult,
        function(error) {
          alert(error.message);
        });
    },
    closePopup() {
      let popup = document.querySelector(".popupHint");
      popup.style.bottom = "-450px";
    },
    showPopup() {
      let popup = document.querySelector(".popupHint");
      popup.style.bottom = "0";
    },
    closePopup2() {
      let popup = document.querySelectorAll(".popupHint")[1];
      popup.style.bottom = "-350px";
    },
    showPopup2() {
      let popup = document.querySelectorAll(".popupHint")[1];
      popup.style.bottom = "0";
    },
    newRoute() {
      this.createRoute(0.15, 0.2);
    }
  }
}
</script>

<style scoped>
#quest {
  overflow: hidden;
}

#map {
  padding-bottom: 0!important;
}

.popupHint {
  position: absolute;
  bottom: -450px;
  background-color: #fff;
  height: 450px;
  width: 100%;
  z-index: 1000;
  box-shadow: 0 4px 64px rgba(0, 0, 0, 0.25);
  border-radius: 24px 24px 0 0;
  transition: all 0.5s ease-out;
  padding: 20px 16px 0 16px;
}

.popupHint2 {
  height: 350px;
}

.navBar {
  position: absolute;
  bottom: 8px;
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.1);
  background-color: #fff;
  border-radius: 24px;
  width: calc(50% - 24px);
  margin: 0 12px;
  z-index: 1000;
  height: 64px;
  display: flex;
  align-items: center;
}

.backBlock {
  top: calc(50% - 14px);
}

.backButton {
  transform: rotate(180deg);
  margin-left: 12px;
}

.infoBtn {
  margin-left: 64px;
}

.number {
  font-family: SF Pro Text, sans-serif;
  font-style: normal;
  font-weight: 500;
  font-size: 36px;
  line-height: 43px;
  text-align: center;
  color: #000000;
}

.primary {
  width: calc(100% - 24px);
  margin: 0 12px!important;
  border: none;
}

.logOut {
  font-family: SF Pro Text, sans-serif;
  font-style: normal;
  font-weight: 500;
  font-size: 18px;
  margin-top: 16px;
  line-height: 20px;
  border: none;
  background: none;
  text-decoration: none;
}

.logOut:active, .logOut:focus {
  outline: none;
  box-shadow: 0 0 4px #FF5F54;
}

.logOut a {
  text-decoration: none;
  color: #FF5F54;
}

.liker {
  background: rgba(1, 122, 255, 0.2);
  border-radius: 8px;
  width: fit-content;
}

.like {
  font-size: 16px;
  border-right: 1px solid #89B8EE;
  text-decoration: none!important;
}
</style>
