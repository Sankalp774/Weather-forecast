# Weather-forecast
Welcome to the Weather Forecast Teller website! This project aims to provide users with up-to-date weather forecasts for their desired locations.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>*{
        color: rgb(7, 1, 1);
        background: rgb(7, 200, 243);
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    
    #cityInput, #cityName, #inputContainer,button{
        margin: 3px;
    padding:5px;
    text-align:center;
    font-size:20px;
    font-weight:bold;
    }
    
    #weatherContainer{
        position: absolute;
        top: 70%;
        left: 50%;
        margin-right: -50%;
        transform: translate(-50%, -50%);
        height: 300px;
        width: 1300px;
        border: 5px solid rgba(97, 95, 95, 0.829);    
        border-radius: 10px;
    }
    
    #iconsContainer{
        position: absolute;
        top: 50%;
        left: 50%;
        margin-right: -50%;
        transform: translate(-50%, -50%);
        height: 240px;
        width: 1200px;    
        border: 5px solid rgb(31, 82, 82);    
        border-radius: 10px;
    }
    
    .icons{
        display: inline-bock;
        float: left;
        height: 200px;
        width: 190px;
        margin: 20px;
        border: 5px solid rgb(48, 47, 47);
        border-radius: 10px;
    }
    
    .image{
        height: 140px;
        width: 100%;
    }
    
    .imgClass{
        height: 140px;
        width: 100%;
    }
    
    .weather{
        margin: 5px;
       /*  background-color: rgb(106, 215, 255); */
        border-radius: 5px;
        text-align: center;
        font-weight: bold;
    }
    
    .minValues{
        text-align: center;
        display: inline-block;
        border-radius: 5px;
        height: 25px;
        width: 85px;
        margin: 0;
        margin-bottom: 5px;
        margin-left: 5px;
    }
    
    
    .maxValues{
        text-align: center;
        display: inline-block;
        border-radius: 5px;
        height: 25px;
        width: 85px;
        margin: 0;
        margin-bottom: 5px;
        margin-left: 5px;
    }</style>
    <title>Document</title>
</head>
<body onload="DefaultScreen()">
    <center>
        <h1 id="Para1">5 Days Weather Forecast</h1>
        <p id="inputContainer">City: <input type="text" id="cityInput"></p>
        <button type="button" onclick="GetInfo()">Click Me</button>        
        <h2 id="cityName">---London---</h2>
    </center>
    
    <div id = "weatherContainer">
        <div id="iconsContainer">    
            <div class = "icons">
                <p class="weather" id="day1"></p>
                <div class="image"><img src="dots.png" class="imgClass" id="img1"></div>
                <p class="minValues" id="day1Min">Loading...</p>
                <p class="maxValues" id="day1Max">Loading...</p>
            </div>
            <div class = "icons">
                <p class="weather" id="day2"></p>
                <div class="image"><img src="dots.png" class="imgClass" id="img2"></div>
                <p class="minValues" id="day2Min">Loading...</p>
                <p class="maxValues" id="day2Max">Loading...</p>
            </div>
            <div class = "icons">
                <p class="weather" id="day3"></p>
                <div class="image"><img src="dots.png" class="imgClass" id="img3"></div>
                <p class="minValues" id="day3Min">Loading...</p>
                <p class="maxValues" id="day3Max">Loading...</p>
            </div>
            <div class = "icons">
                <p class="weather" id="day4"></p>
                <div class="image"><img src="dots.png" class="imgClass" id="img4"></div>
                <p class="minValues" id="day4Min">Loading...</p>
                <p class="maxValues" id="day4Max">Loading...</p>
            </div>
            <div class = "icons">
                <p class="weather" id="day5"></p>
                <div class="image"><img src="dots.png" class="imgClass" id="img5"></div>
                <p class="minValues" id="day5Min">Loading...</p>
                <p class="maxValues" id="day5Max">Loading...</p>
            </div>
        </div>
    </div>


        <script src="main.js">
            function GetInfo() {

var newName = document.getElementById("cityInput");
var cityName = document.getElementById("cityName");
cityName.innerHTML = "--"+newName.value+"--";

fetch('https://api.openweathermap.org/data/2.5/forecast?q='+newName.value+'&appid=32ba0bfed592484379e51106cef3f204')
.then(response => response.json())
.then(data => {

//Getting the min and max values for each day
for(i = 0; i<5; i++){
    document.getElementById("day" + (i+1) + "Min").innerHTML = "Min: " + Number(data.list[i].main.temp_min - 273.15).toFixed(1)+ "°";
    //Number(1.3450001).toFixed(2); // 1.35
}

for(i = 0; i<5; i++){
    document.getElementById("day" + (i+1) + "Max").innerHTML = "Max: " + Number(data.list[i].main.temp_max - 273.15).toFixed(2) + "°";
}
//------------------------------------------------------------

//Getting Weather Icons
 for(i = 0; i<5; i++){
    document.getElementById("img" + (i+1)).src = "http://openweathermap.org/img/wn/"+
    data.list[i].weather[0].icon
    +".png";
}
//------------------------------------------------------------
console.log(data)


})

.catch(err => alert("Something Went Wrong: Try Checking Your Internet Coneciton"))
}

function DefaultScreen(){
document.getElementById("cityInput").defaultValue = "London";
GetInfo();
}


//Getting and displaying the text for the upcoming five days of the week
var d = new Date();
var weekday = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday",];

//Function to get the correct integer for the index of the days array
function CheckDay(day){
if(day + d.getDay() > 6){
    return day + d.getDay() - 7;
}
else{
    return day + d.getDay();
}
}

for(i = 0; i<5; i++){
    document.getElementById("day" + (i+1)).innerHTML = weekday[CheckDay(i)];
}

        </script>


</body>
</html>
