# มาทำแอพพยากรณ์อากาศด้วย Vue.js

[Source](https://medium.com/@kongruksiamza/%E0%B8%A1%E0%B8%B2%E0%B8%97%E0%B8%B3%E0%B9%81%E0%B8%AD%E0%B8%9E%E0%B8%9E%E0%B8%A2%E0%B8%B2%E0%B8%81%E0%B8%A3%E0%B8%93%E0%B9%8C%E0%B8%AD%E0%B8%B2%E0%B8%81%E0%B8%B2%E0%B8%A8%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-vue-js-32531b0bd420)

**Youtube :** [https://www.youtube.com/watch?v=dtWLsVxVjuQ](https://www.youtube.com/watch?v=dtWLsVxVjuQ)

**Index.html**

```markup
<script src="[https://cdn.jsdelivr.net/npm/vue/dist/vue.js](https://cdn.jsdelivr.net/npm/vue/dist/vue.js)"></script>  
<script src="[https://unpkg.com/axios/dist/axios.min.js](https://unpkg.com/axios/dist/axios.min.js)"></script>  
  <style>  
    * {  
      box-sizing: border-box;  
    }  
    body {  
      margin: 0;  
      padding: 0;  
      font-size: 16px;  
      font-family: arial, sans-serif;  
      color: #878787;  
    }select {  
      padding: 5px 10px;  
      width: 150px;  
      height: 25px;  
      font-size: 13px;  
      color: #555;  
      border: 1px solid #ccc;  
    }#weather {  
      margin: auto;  
      max-width: 632px;  
    }#setting {  
      margin: 20px 0;  
    }#display {  
      padding: 20px 16px 24px 16px;  
      box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.16), 0 0 0 1px rgba(0, 0, 0, 0.08);  
      background-color: #ffffff;  
    }#top {  
      margin-bottom: 20px;  
    }#top .location {  
      font-size: 24px;  
      line-height: 1.2;  
    }#top .time {  
      font-size: 16px;  
      line-height: 2;  
    }#top .status {  
      font-size: 13px;  
      line-height: 1.4  
    }#left{  
      color: #212121;  
    }#left.thumbnail {  
      float: left;  
      height: 64px;  
      width: 64px;  
    }#left.temperature {  
      float: left;  
      margin-top: -3px;  
      padding-left: 10px;  
      font-size: 64px;  
    }#left.unit {  
      float: left;  
      margin-top: 6px;  
      font-size: 20px;  
    }#right {  
      float: right;  
      padding-left: 5px;  
      line-height: 22px;  
      padding-top: 2px;  
      min-width: 43%;  
      font-weight: lighter;  
    }#forecast {  
      padding-top: 10px;  
      clear: both;  
    }#forecast ul {  
      padding: 0;  
      margin: 15px 0 5px 0;  
    }#forecast ul li {  
      display: inline-block;  
      height: 90px;  
      width: 73px;  
      text-align: center;  
      line-height: 1;  
    }  
</style>
```

**app.js**

```javascript
new Vue({  
  el: "#weather",  
  data: {  
    woeid: "1225448",  
    location: "",  
    status: "",  
    time: "",  
    temperature: "0",  
    humidity: "0",  
    wind: "0",  
    pressure: "0",  
    forecast: [],  
    error: false  
  },  
  mounted: function() {  
    this.changeLocation();  
  },  
  computed: {  
    displayDate: function() {  
      return this.time.slice(0, 16);  
    }  
  },  
  methods: {  
    changeLocation: function() {  
      var api =  
        "[https://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20%3D%20](https://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20%3D%20)" +  
        this.woeid +  
      "%20and%20u%20%3D%20'c'&format=json&env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys";  
      var self = this;  
      axios  
        .get(api)  
        .then(function(response) {  
          var channel = response.data.query.results.channel;  
          if (channel) {  
            self.location = channel.location.city + ", " + channel.location.country;  
            self.time = channel.item.pubDate;  
            self.status = channel.item.condition.text;  
            self.temperature = channel.item.condition.temp;  
            self.humidity = channel.atmosphere.humidity;  
            self.pressure = channel.atmosphere.pressure;  
            self.wind = channel.wind.speed;  
            self.forecast = channel.item.forecast;  
          } else {  
            self.error = true;  
          }  
        })  
        .catch(function(error) {  
          self.error = true;  
        });  
    },  
    getThumbnail: function(status, size) {  
      switch (status.toLowerCase()) {  
        case "hot":  
          return "[https://ssl.gstatic.com/onebox/weather/](https://ssl.gstatic.com/onebox/weather/)" + size + "/hot.png";  
        case "sunny":  
        case "mostly sunny":  
          return "[https://ssl.gstatic.com/onebox/weather/](https://ssl.gstatic.com/onebox/weather/)" + size + "/sunny.png";  
        case "thunderstorms":  
        case "severe thunderstorms":  
          return "[https://ssl.gstatic.com/onebox/weather/](https://ssl.gstatic.com/onebox/weather/)" + size + "/thunderstorms.png";  
        case "scattered thunderstorms":  
          return "[https://ssl.gstatic.com/onebox/weather/](https://ssl.gstatic.com/onebox/weather/)" + size + "/rain_s_cloudy.png";  
        case "partly cloudy":  
        case "mostly cloudy":  
          return "[https://ssl.gstatic.com/onebox/weather/](https://ssl.gstatic.com/onebox/weather/)" + size + "/partly_cloudy.png";  
        case "cloudy":  
          return "[https://ssl.gstatic.com/onebox/weather/](https://ssl.gstatic.com/onebox/weather/)" + size + "/cloudy.png";  
        case "showers":  
        case "scattered showers":  
          return "[https://ssl.gstatic.com/onebox/weather/](https://ssl.gstatic.com/onebox/weather/)" + size + "/rain_light.png";  
        case "rain":  
          return "[https://ssl.gstatic.com/onebox/weather/](https://ssl.gstatic.com/onebox/weather/)" + size + "/rain.png";  
        case "snow":  
        case "heavy snow":  
        case "snow flurries":  
        case "blowing snow":  
          return "[https://ssl.gstatic.com/onebox/weather/](https://ssl.gstatic.com/onebox/weather/)" + size + "/snow.png";  
        case "sleet":  
          return "[https://ssl.gstatic.com/onebox/weather/](https://ssl.gstatic.com/onebox/weather/)" + size + "/sleet.png";  
        case "windy":  
          return "[https://ssl.gstatic.com/onebox/weather/](https://ssl.gstatic.com/onebox/weather/)" + size + "/windy.png";  
        default:  
          return "[https://ssl.gstatic.com/onebox/weather/](https://ssl.gstatic.com/onebox/weather/)" + size + "/cloudy.png";  
      }  
    }  
  }  
});
```

