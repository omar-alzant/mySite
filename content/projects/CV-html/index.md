---
title: "CV"
date: 2022-06-11
draft: false
blog_tags: ["html", "css"]
status: "html css"
weight: 22
summary: "In this project, we will be creating a small CV application.
"
links:
    external_link:
        text: "Some external link"
        icon: "fas fa-external-link-alt"
        href: "https://www.theodinproject.com/lessons/node-path-javascript-cv-application"
        weight: 1
    another_link:
        text: "Another github link"
        icon: "fab alt brands fa-github"
        href: "https://github.com/omar-alzant/myCV"
        weight: 2
---


</br>
</br>

  **Idea :** </br>
  <em>
    " Learning a new technology is never easy. Along the way you might think: “Well, I could easily implement this in plain Javascript”. BUT don’t let that demotivate you. If you keep pushing, you will end up far more productive than you were before with the ability to add a new skill to your skillset".
  </em>

***
</br>
</br>

**Tip:**
 </br>
 If you’re confused on how to deploy using GitHub Pages, take a look at this 
 [article](https://blog.usejournal.com/how-to-deploy-your-react-app-into-github-pages-b2c96292b18e).
 

***

</br>
</br>

## Steps:

1- Create a new project using `npx create-react-app cv-project`. If you need a reminder on how it works, check out the previous lessons. Don’t forget to setup a GitHub repository for your project, to push your progress.

2- Remove the boilerplate code created by `create-react-app`.

3- You should use class components for this project. You’re going to find a lot of code written using class components and this practical experience will help you understand it when encountered.

4- Think about how to structure your application into components. Your application should include:

- A section to add general information like name, email, phone number.

- A section to add your educational experience (school name, title of study, date of study)

- A section to add practical experience (company name, position title, main tasks of your jobs, date from and until when you worked for that company)


***

</br>
</br>

Code -Html- :


```html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>Omar-j-Alzant</title>

    <link rel="shortcut icon"  href="./contact-book (1).png">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">

    <!-- custom css -->
    <link href="./style.css" rel="stylesheet">

  </head>
  <body>
    <div class="resume-wrapper">

      <!-- header -->
      <header>
        <h1 class="heading-container">Omar Alzant</h1>
        <h2 class="name-container">WebDev-fullStack JS</h2>
        <div class="job-container">
          <h3>Lebanon, Tripoli</h3>
          <h3 >22/09/1997</h3>
        </div>
        <!-- <button onclick="myFunction()">Toggle dark mode</button> -->

        <div class="profile-picture">
          <img src="./prof.png" loading="lazy"  alt="myphoto">
        </div>
        <div class="contact-container">
          <ul class="contact-list">
            <li>
              <a href="">+96176138514</a>
              <span><i class="fa fa-phone" aria-hidden="true"></i></span>
            </li>
            <li>
              <a href="alzanatomar.19@gmail.com">alzanatomar.19@gmail.com</a>
              <span><i class="fa fa-envelope-o" aria-hidden="true"></i></span>
            </li>
            <li>
              <a href="https://omar-alzant.github.io/My-portfolio/" target="_blank">My portfolio</a>
              <span><i class="fa fa-globe" aria-hidden="true"></i></span>
            </li>
            <li>
              <a href="https://github.com/omar-alzant" target="_blank">My github page</a>
              <span><i class="fa fa-github" aria-hidden="true"></i></span>
            </li>
          </ul>
        </div>
      </header><!-- header -->

      <!-- main -->
      <section id="main">
        <div class="resume-item-wrapper">

          <!-- experince -->
          <section class="resume-item experience">
            <div class="inner">
              <h2>experience</h2>
              <ul>

                <li>
                  <h3>Google-Script</h3>
                  <h4 class="company">myHome</h4>
                  <span class="date">Apr 2022 - Present</span>
                  <p class="detail">
                    Write code to enter data, analyze it, and then sort it using gScript for google sheet.
                    </p>
                </li>
                <li>
                  <h3>Robotic</h3>
                  <h4 class="company">AlManar-Islamic-School</h4>
                  <span class="date">Jun 2019 - Aug 2019</span>
                  <p class="detail">
                    Teach how to program the robot.
                  </p>
                </li>
              </ul>
            </div>
          </section><!-- experince -->


          <div class="resume-item-wrapper">

            <!-- experince -->
            <section class="resume-item experience">
              <div class="inner">
                <h2>Education</h2>
                <ul>
                  <li>
                    <h3>The Odin Project -online-</h3>
                    <h4 class="company">WebSite</h4>
                    <span class="date">Jun 2021 - present</span>
                  </li>
                  <li>
                    <h3>CCNAv7 -ITN</h3>
                    <h4 class="company">LASeR-Tripoli</h4>
                    <span class="date">Nov 2021 - Jan 2022</span>
                  </li>
                  <li>
                    <h3>CS50 -Intro to CS -online-</h3>
                    <h4 class="company">Harvard University</h4>
                    <span class="date">Apr 2021 - Jun 2021</span>
                  </li>
                  <li>
                    <h3>Master1 Electronic Industrial</h3>
                    <h4 class="company">Lebanese University</h4>
                    <span class="date">Set 2018 - Jun 2021</span>
                  </li>
                  <li>
                    <h3>B.S. Electronic Industrial</h3>
                    <h4 class="company">Lebanese University</h4>
                    <span class="date">Set 2016 - Jun 2018</span>
                  </li>

                </ul>
              </div>
  

          <!-- project -->
          <section class="resume-item project">
            <div class="inner">
              <h2>project</h2>
              <ul>
                <li>
                  <h3><a href="https://github.com/omar-alzant/Blogs" target="_blank">Some Blogs</a></h3>
                  <p class="detail">
                    I Create two blogs :
                    <a href="https://github.com/omar-alzant/Blogs/blob/main/Array.md">Array</a> , 
                    <a href="https://github.com/omar-alzant/Blogs/blob/main/DesignPattern.md">DesignPatterns</a>
                  </p>
                  <p class="tags">#markdown </p>
                </li>

                <li>
                  <h3><a href="https://github.com/omar-alzant/Admin-Dashboard" target="_blank">Dashboard form.</a></h3>
                  <p class="detail">
                    A simple form for dashboard page using HTML5 CSS3 and JavaScript 
                    <a  href="https://omar-alzant.github.io/Admin-Dashboard/"> Live view</a>
                    .
                  </p>
                  <p class="tags">#HTML5 #CSS3 #JS</p>
                </li>
                <li>
                  <h3><a href="https://github.com/omar-alzant/esp-gas-finalproject-CS50" target="_blank">ESPic-webpage</a></h3>
                  <p class="detail">
                    Mixing electronics and the web to get data of DHTsensor and fetch it to web page.
                  </p>
                  <p class="tags">#HTML5 #CSS3 #XML #Arduino </p>
                </li>
                <li>
                  <h3><a href="https://github.com/omar-alzant/My-portfolio" target="_blank">Portfolio.</a></h3>
                  <p class="detail">
                    Writting my own Portfolio using web programs-js/ CSS/ HTML.
                  </p>
                  <p class="tags">#HTML5 #CSS3 #JS</p>
                </li>
                <li>
                  <h3><a href="https://github.com/omar-alzant/weather-App" target="_blank">Weather-API.</a></h3>
                  <p class="detail">
                    Ease of searching for the weather for any country around the world, 
                    <a href="https://omar-alzant.github.io/weather-app/">Live view</a>
                    .                                    </p>
                  <p class="tags">#HTML5 #CSS3 #JS #API</p>
                </li>
                <li>
                  <h3><a href="https://github.com/omar-alzant/dna-searching" target="_blank">DNA Search.</a></h3>
                  <p class="detail">
                    Search for the same dna type from csv file, using Python.
                  </p>
                  <p class="tags">#Python</p>
                </li>
                <li>
                  <h3>Nrf-Tx-Rx</h3>
                  <p class="detail">
                    Using nrf wiht arduino transmitter and receiver to send data.
                  </p>
                  <p class="tags">#Arduino</p>
                </li>
                <li>
                  <h3>WebCam-Matlab</h3>
                  <p class="detail">
                    Make and program a small robot, and control it with webCamera linking with matlab app to recognize the image.
                  </p>
                  <p class="tags">#Arduino #Matlab </p>
                </li>
                <li>
                  <h3>dsPic - AVR </h3>
                  <p class="detail">
                    Program different type of uP and make some circuit. 
                  </p>
                  <p class="tags">#MicroC #MPLab </p>
                </li>
              </ul>
            </div>
          </section><!-- project -->

          <!-- skill -->
          <section class="resume-item skill">
            <div class="inner">
              <h2>Skill</h2>
              <ul>
             
                <li>
                  <h3>JS, CSS3, API, XML, Flask</h3>
                  <div class="skill-bar">
                    <span class="bar" style="width: 80% ;"></span>
                  </div>
                </li>
                <li>
                  <h3>Microsoft Office</h3>
                  <div class="skill-bar">
                    <span class="bar" style="width: 70% ;"></span>
                  </div>
                </li>
                <li>
                  <h3>C, Cpp, Python,SQL</h3>
                  <div class="skill-bar">
                    <span class="bar" style="width: 60% ;"></span>
                  </div>
                </li>
                <li>
                  <h3>Arduino, Labview, Proteus, matLab, MPLab</h3>
                  <div class="skill-bar">
                    <span class="bar" style="width: 70% ;"></span>
                  </div>
                </li>
                <li>
                  <h3>Grafcet, MicroC, RaspPy, FlowCode</h3>
                  <div class="skill-bar">
                    <span class="bar" style="width: 80% ;"></span>
                  </div>
                </li>
              </ul>
            </div>
          </section><!-- skill -->

          <section class="resume-item lang">
            <div class="inner">
              <h2>Language</h2>
              <ul>
                <li>
                  <h3>Arabic</h3>
                  <div class="lang-bar">
                    <span class="bar" style="width: 100% ;"></span>
                  </div>
                </li>
                <li>
                  <h3>Franch</h3>
                  <div class="lang-bar">
                    <span class="bar" style="width: 50% ;"></span>
                  </div>
                </li>
                <li>
                  <h3>English</h3>
                  <div class="lang-bar">
                    <span class="bar" style="width: 65% ;"></span>
                  </div>
                </li>
                  
        </div>
      </section><!-- main -->

      <!-- footer -->
      <footer>
        <p>
          © 2022           
           <a href="https://github.com/omar-alzant" target="-_blank">OjZ</a>. All rights reserved.
        </p>
      </footer><!-- footer -->
      <!-- <script>
        function myFunction() {
           var element = document.body;
           element.classList.toggle("dark-mode");
        }
        </script> -->
        
    </div>
  </body>
</html>

```

***

</br>
</br>

Code -CSS- :

```css


* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  margin: 0;
}

a {
  color: rgb(247, 114, 114);
  text-decoration: none;
}

ul {
  list-style: none;
}

body {
  margin: 0;
  padding: 0;
  background: lightskyblue;
  color: #333;
}

.resume-wrapper {
  position: relative;
  width: 960px;
  margin: 30px auto 60px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  background: rgba(251, 248, 248, 0.857);
}

/* header */
header {
  position: relative;
  padding: 30px;
  border-bottom: 1px solid #ededed;
}
header h1 {
  position: absolute;
  bottom: 60px;
  right: 180px;
  z-index: 1;
  font-size: 42px;
}
header .name-container {
  position: absolute;
  left: 770px;
  bottom: 0;
  z-index: 1;
  height: 30px;
  padding-left: 10px;
  margin: 0;
  font-size: 18px;
  line-height: 30px;
}
header .job-container {
  position: absolute;
  left: 770px;
  bottom: -20px;
  z-index: 1;
  height: 20px;
  padding-left: 10px;
  margin: 0;
  color: #666;
  font-size: 14px;
  font-weight: normal;
  line-height: 20px;
}
header .profile-picture {
  position: absolute;
  right: 190px;
  bottom: -50px;
  z-index: 2;
  width: 100px;
  height: 100px;
  border-radius: 50%;
}
header .profile-picture img {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  border: 1px solid rgba(0, 0, 0, 0.1);
}
header .contact-container {
  position: relative;
  top: 0px;
  left: 30px;
}
header .contact-container .contact-list li {
  position: relative;
  height: 25px;
  padding-left: 25px;
  color: #666;
  font-size: 13px;
  line-height: 25px;
  text-align: left;
}
header .contact-container .contact-list li span {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  width: 25px;
  height: 25px;
  text-align: center;
}

/* main */
#main {
  position: relative;
  padding: 2px;
}

#main > .resume-item-wrapper {
  position: relative;
  top: 0;
  left: 0;
  width: 720px;
  padding: 75px 0 40px;
  border-right: 1px solid #ededed;
}

#main .resume-item {
  position: relative;
  padding: 10px;
  margin-bottom: 60px;
}
#main .resume-item .inner {
  padding-bottom: 30px;
  border-bottom: 1px solid #ededed;
}
#main .resume-item h2 {
  position: absolute;
  top: -10px;
  right: -240px;
  z-index: 1;
  width: 240px;
  height: 30px;
  padding: 0 30px;
  font-size: 24px;
  text-align: left;
  text-transform: capitalize;
}
#main ul li {
  position: relative;
  margin: 0 0 30px;
}

/* experience */
.experience h3 {
  font-size: 18px;
}
.experience .company {
  margin: 0 0 10px;
  color: #959595;
  font-size: 13px;
  font-weight: normal;
}
.experience .date {
  position: absolute;
  top: 5px;
  right: 0;
  color: rgb(131, 127, 127);
  font-size: 12px;
}
.experience .detail {
  font-size: 14px;
}

/* project */
.project ul li {
  font-size: 0;
  line-height: 16px;
}
.project h3 {
  position: relative;
  display: inline;
  color: #666;
  font-size: 16px;
}
.project h3::after {
  content: " - ";
}
.project .detail {
  display: inline;
  font-size: 14px;
}
.project .tags {
  font-size: 12px;
  color: #999;
}

/* skill */
.skill {
  margin-bottom: 0 !important ;
}
.skill ul li {
  height: 15px;
}
.skill h3 {
  float: left;
  width: 30%;
  height: 100%;
  font-size: 14px;
  font-weight: normal;
  line-height: 14px;
}
.skill .skill-bar {
  float: left;
  width: 70%;
  height: 100%;
  background: #f5f5f5;
}
.skill .skill-bar .bar {
  display: block;
  width: 60%;
  height: 100%;
  background: #666;
}

/*  Lang */
.lang {
  margin-bottom: 0 !important ;
}
.lang ul li {
  height: 15px;
}
.lang h3 {
  float: left;
  width: 30%;
  height: 100%;
  font-size: 14px;
  font-weight: normal;
  line-height: 14px;
}
.lang .lang-bar {
  float: left;
  width: 70%;
  height: 100%;
  background: #f5f5f5;
}
.lang .lang-bar .bar {
  display: block;
  width: 60%;
  height: 100%;
  background: rgb(118, 226, 226);
}

/* footer */
footer {
  position: absolute;
  bottom: -30px;
  left: 0;
  width: 100%;
  padding: 0 30px;
  font-size: 12px;
  text-align: left;
  color: rgb(11, 10, 10);
}
footer a {
  font-weight: bold;
}

```