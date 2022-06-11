---
title: "Weather API"
date: 2022-06-11
draft: false
project_tags: ["html","css","js"]
status: "html css js"
weight: 19
summary: "Display  weather  of search API."
links:
    external_link:
        text: "Some external link"
        icon: "fas fa-external-link-alt"
        href: "https://www.theodinproject.com/lessons/node-path-javascript-weather-app"
        weight: 1
    another_link:
        text: "Another github link"
        icon: "fab alt brands fa-github"
        href: "https://github.com/omar-alzant/weather-app"
        weight: 2
---

</br>
</br>

We use :

<img src="./all.png" alt="use-icon" style="max-width: 700px; margin: 10px;">

---

</br>
</br>

- In this project we  want to  change the look of the page based on the data ,by adding images that describe the weather. (we use the Giphy API to find appropriate weather-related gifs and display them).

- We use promises this code.

- You can
<a href="https://omar-alzant.github.io/weather-app/">
Try-it
</a>.

---

</br>
</br>

The result :

<img src="./admin.png" alt="result-icon" style="max-width: 700px;">

***

</br>
</br>

## API Keys, Secret and Security :

- Not all APIs are free, and depending on how they’re set up, they can cost money per use. This makes them a prime target for people looking to use the API without paying by using your API key. They can also be rate-limited, and if someone has access to your API key they can use up all of your uses.

- One way to prevent this issue is to store your API keys on the server and never send them to the frontend in the first place, this is often done using environment variables and it makes the key available only on the server the code is deployed to.

- When talking about API keys and security you’ll often hear “Never trust the client” (client meaning the frontend). Often this means not to trust that data coming from the client is valid, but it also means that you cannot trust anything we send to the client.

- !!!  when you leak an API key, Github will alert you that you have committed an API key publicly.


***

</br>
</br>



Code -CSS- :

```css
@font-face {
    font-family: 'own';
    src: url(./SansitaSwashed-VariableFont_wght.ttf);
        /* src: url(../dist/SansitaSwashed-VariableFont_wght.ttf); */
}

body {
  
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  margin: 0;
  font-family: 'own';
  background-repeat: no-repeat;
  background-size: cover;
}
 

.tempUnit{
  display: flex;
  gap: 10px;
}

#unit{
  cursor: pointer;
}

.card {
  /* background-color: rgba(238, 238, 238, 0.548); */
  padding: 5vw;
  border-radius: 15%;
  width: 100%;
  max-width: 400px;
  /* color: rgb(0, 0, 0); */
}
h1{
    margin: 0;
}

input.search-bar {
  border: none;
  border-radius: 18px;
  padding: 15px;
  outline: none;
  color: white;
  /* margin: 2em; */
  background-color: #101010d0;
  font-family: 'own';
  align-items: center;  
    width: calc(100% - 45px);
}

button {
  border: none;
  outline: none;
  border-radius: 50%;
  height: 2.5em;
  width: 3em;
  background-color: #101010d0;
  color: white;
  cursor: pointer;
  transition: 0.2s ease-in-out;
}

button:hover{
    background-color: #2b2b2bd0;
}

```

***

</br>
</br>

Code -JS- :

```javascript
// https://api.openweathermap.org/data/2.5/weather?q=
//  {city name}
//  &appid=
//  {API key}
// &units={metric-C- or imperial-F-}
// $lang={lang}




let weather ={
    apikey: 'Your-API-Key',

        //  Fetching function :

        fetchWeather: function (city) {
            fetch(
              "https://api.openweathermap.org/data/2.5/weather?q=" +
                city +
                "&units=metric&appid=" +
                this.apikey
            )
              .then((response) => {
                if (!response.ok) {
                  alert("No weather found.");
                  throw new Error("No weather found.");
                }
                return response.json();
              })
              .then((data) => this.displayWeather(data));
          },

        // End of fetching function 


        //   Display Function : 

        displayWeather : (data)=>{
            const {name} = data;
            const {icon,description} = data.weather[0];
            const {temp,humidity} = data.main;
            const {speed} = data.wind;
            let time = 'night';

            document.querySelector('.city').innerHTML = 'Weather in '+name;
            document.querySelector('.icon').src  =   'https://openweathermap.org/img/wn/'+icon+'.png';
            document.querySelector('.description').innerHTML = description;
            document.querySelector('.temp').innerHTML = temp;
            document.querySelector('.humidity').innerHTML = 'Humidity:  '+ humidity + '%';
            document.querySelector('.wind').innerHTML = 'Wind speed:   ' + speed + 'km/h';
            let card = document.querySelector('.card');
            // let sec = document.getElementById('sec');
                // unit = document.getElementById("unit");



            card.style.backgroundColor = 'rgba(238, 238, 238, 0.548)';
            card.style.color = 'black';

            str = description.replace(/\s/g, '');

            if(icon.match(/^(\d{2}(d))$/)) 
            {
                time = 'day'; 
                card.style.backgroundColor = 'rgba(17, 34, 51, 0.548)';
                card.style.color = 'white'
            }

        //  API background :

             let bckurl = '-' + str + '-' + time ;
        
            // console.log(time);
        
            document.body.style.backgroundImage =       
             "url('https://source.unsplash.com/1600x900/?weather" + bckurl + "')";
           // "url(./weather.png)";
        //  End of API bck 

        // End of Display Func 
        
      },



        //   Search Function :

        search: function () {
            this.fetchWeather(document.querySelector(".search-bar").value);
          },

        //   End of Search Function 


        //   End of weather object ;) 
        };

        document.querySelector(".search button").addEventListener("click", function () {
          weather.search();
        });

        document
          .querySelector(".search-bar")
          .addEventListener("keyup", function (event) {
            if (event.key == "Enter") {
              weather.search();
            }
          });
      
        weather.fetchWeather("Beirut");

```

---

</br>
</br>

Code -Html- :

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="shortcut icon" href=""/>
    <link rel="stylesheet" href="./style.css">
    <title>Weather-API-</title>
</head>
<body>
    
    <div class="card">
        <div class="search">
            <input type="search"  class="search-bar" placeholder="Search">
            <button>
                <svg stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 1024 1024" height="1.5em" width="2em" xmlns="http://www.w3.org/2000/svg"><path d="M909.6 854.5L649.9 594.8C690.2 542.7 712 479 712 412c0-80.2-31.3-155.4-87.9-212.1-56.6-56.7-132-87.9-212.1-87.9s-155.5 31.3-212.1 87.9C143.2 256.5 112 331.8 112 412c0 80.1 31.3 155.5 87.9 212.1C256.5 680.8 331.8 712 412 712c67 0 130.6-21.8 182.7-62l259.7 259.6a8.2 8.2 0 0 0 11.6 0l43.6-43.5a8.2 8.2 0 0 0 0-11.6zM570.4 570.4C528 612.7 471.8 636 412 636s-116-23.3-158.4-65.6C211.3 528 188 471.8 188 412s23.3-116.1 65.6-158.4C296 211.3 352.2 188 412 188s116.1 23.2 158.4 65.6S636 352.2 636 412s-23.3 116.1-65.6 158.4z"></path></svg>
            </button>
        </div>

        <div class="weather loading">
            <h2 class="city">Weather in Denver</h2>
            <div class="tempUnit">
                <h1 class="temp"></h1> 
                <h1 id="unitC">°C</h1>   <!--°C -->
                <!-- <h1 id="unitF">°F</h1>   °F -->
            </div>   
            <div class="flex">
              <img src="https://openweathermap.org/img/wn/04n.png" alt="description-icon" class="icon" />
              <div class="description"></div>
            </div>
            <div class="humidity">Humidity: </div>
            <div class="wind">Wind speed: </div>
            </div>
          </div>
<script src="./index.js"></script>
    <!-- <script src="../dist/main.js"></script> -->
</body>
</html>
```

***

</br>
</br>
