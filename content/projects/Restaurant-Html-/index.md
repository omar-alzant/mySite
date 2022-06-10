---
title: "Restaurant Page"
date: 2022-06-10
draft: false
project_tags: ["html","css","js","webpack"]
status: "html css js webpack"
weight: 17
summary: "We’re going to build a browser version of something between a sketchpad and an Etch-A-Sketch.
"
links:
    external_link:
        text: "Some external link"
        icon: "fas fa-external-link-alt"
        href: "https://www.theodinproject.com/lessons/node-path-javascript-restaurant-page"
        weight: 1
    another_link:
        text: "Another github link"
        icon: "fab alt brands fa-github"
        href: "#"
        weight: 2
---


</br>
</br>

We use : 

<img src="./all.png" alt="use-icon" style="max-width: 700px; margin: 10px;">

<img src="./web.png" alt="use-icon" style="max-width: 700px; margin: 10px;">

***

</br>
</br>

Tutorial :

- <a href="https://webpack.js.org/guides/getting-started/#using-a-configuration">
  Getting started with webpack
</a>.

- <a href="https://gist.github.com/cobyism/4730490">
  Deploying a subfolder to Github Page
</a>.

***

</br>
</br>

<strong>
  This project is incomplete (index.js).
</strong>

***

</br>
</br>


Code -Home.js- :

```javascript

  "use strict"

  const  h = [
            {el: "p", text: "We offer you the most delicious Levantine cuisine cooked by the most skilled local chefs."},
            {el: "p", text: "Order online Or Contact Us.", css: ["marginTop", "5vw"] },
            {el: "img" },
            ];

    let     cont = document.getElementById("content"),
            // imgH = "../dist/img/Mashawi.jpg",
            imgH = "../src/img/Mashawi.jpg",
            homeP = document.createElement("div"),
            homeImg = document.createElement("div");
            homeP.classList.add('home-p');


    export  default function  Home(){
     document.body.classList.add('home');
            h.map( (h)=>{
                let create = document.createElement(`${h.el}`);
                h.text
                  ? (() => {
                      (create.textContent = h.text), console.log("p");
                      h.css
                        ? (() => {
                            create.style.marginTop = `${h.css[1]}`;
                            console.log("css");
                          })()
                        : console.log("css Not found");
                      homeP.appendChild(create);
                    })()
                  : (h.el = "img"
                      ? (() => {
                          console.log("img");
                          create.setAttribute("src", `${imgH}`),
                            create.setAttribute("alt", "image-Home");
                          create.classList.add("home-img");
                          homeImg.appendChild(create);
                        })()
                      : console.log("img not found"));
                cont.appendChild(homeP);
                cont.appendChild(homeImg);
              })
    };  
 
```

***

</br>
</br>


Code -contact.js- :

```javascript

  "use strict"

let c = [   // It should be organized according to the sequence in the entry
        {el:'legend', text:"Contact Email:"},
        {el:"label",  text:'Your-Email:', for:'email'},
        {el:'input',  type:"email", id:'email', placeholder:'example@email.com',css:'control'},
        {el:'label',  text:'Create message:',for:'msg'},
        {el:'textarea',id:"msg"},
        {el:'input', type:'submit', value:"Submit"},
    ];

    document.body.classList.add('contact');
    let create;
    let form  = document.createElement('form'),
        field = document.createElement('fieldset'),
        leg   = document.createElement('legend'),
        lab1  = document.createElement('label'),
        lab2  = document.createElement('label'),
        inp1  = document.createElement('input'),
        sub   = document.createElement('input'),
        text  = document.createElement('textarea');
        // let cont = document.getElementById('content');


        export  default function Contact(){
      inp1.classList.add('control')

      form.setAttribute('action', '#');

      // leg.textContent = "Contact Email:";

      lab1.setAttribute('for','in1'),
      lab1.textContent = "Your-Email:";

      lab2.setAttribute('for','msg');
      lab2.textContent = "Create message:"

      inp1.setAttribute('type','email'),
      inp1.setAttribute('id','in1'),
      inp1.setAttribute('name','email'),
      // inp1.setAttribute('pattern', "[\w\.]+@[a-z]+\.[a-z]{3}"),
      inp1.setAttribute('placeholder','example@email.com');
      // inp1.setAttribute('required');

      sub.setAttribute('type','submit'),
      sub.setAttribute('value','submit');

      text.setAttribute('id','msg'),
      text.setAttribute('name','msg');
      // text.setAttribute('required');

      field.appendChild(leg);

      field.appendChild(lab1),
      field.appendChild(inp1),

      field.appendChild(lab2),
      field.appendChild(text);

      form.appendChild(field),
      form.appendChild(sub);

    return form;
    
  };


```

***

</br>
</br>

Code -menu.js- :

```javascript

'use strict';
let g = [
	{
		title: 'Kabab:',
		// src: "../dist/img/kabab.jpg",
		src: '../src/img/kabab.jpg',
		alt: 'kabab',
		para: 'Chicken, Onion, Garlic, Chili-pepper, Egg, Salt, Garam-masala and Coriander.',
	},
	{
		title: 'Barbecue Chicken:',
		src: '../src/img/dajaj.jpg',
		alt: 'dajaj',
		para: 'spices, crushed-garlic, salt, vinegar, Soy-sauce, Black-papper and Lemon.',
	},
	{
		title: 'Barbecue Meat',
		src: '../src/img/lahmeh.jpg',
		alt: 'lahmeh',
		para: 'Rock-salt, Whole-black-peppercorns, Minced-dried-garlic,Minced-dried-onion, Fennel-seeds, Thyme, Chopped-parsley and Minced-Garlic.',
	},
	{
		title: 'Tawook:',
		src: '../src/img/tawook.jpg',
		alt: 'tawook',
		para: 'Spices, Yogurt, Lemon-Juice and Garlic.',
	},
	{
		title: 'Kaftah:',
		src: '../src/img/kaftah.jpeg',
		alt: 'kaftah',
		para: 'Ground-beef, Onions, Parsley and Spices.',
	},
	{
		title: 'Tabouleh:',
		src: '../src/img/tabouleh.jpg',
		alt: 'tabouleh',
		para: 'Bulgur, Parsley, Tomato, Onion, Bulgur-wheat, Lemon, Olive-oil, Salt, Sprin-Onion, Italian-Parsley, Mint, Black-peppera and Mint-leaves.',
	},
	{
		title: 'Fatouch:',
		src: '../src/img/fatouch.jpg',
		alt: 'fatouch',
		para: 'Tomato, Sumac, Onion, Garlic, Cucumber, Pomegranate-molasses, Lemon, Olive-oil, Parsley, Salt, Bell-pepper, Radish, Balck-pepper, Spring-onion, Mint, Romaine-lettuce, Italian-parsley and Pita-bread.',
	},
];

let m = ['img', 'strong', 'p'];

let gridItem = document.createElement('div'),
	grid = document.createElement('div');
let cont = document.getElementById('content');

export default function Menu() {
	document.body.classList.add('menu');

	g.map((g) => {
		let create;
		m.map((m) => {
			if (m == 'img') {
				create = document.createElement('img');
				create.setAttribute('src', `${g.src}`),
				create.setAttribute('alt', `${g.alt}`);
			}

			if (m == 'strong') {
				create = document.createElement('strong');
				create.textContent = g.title;
				gridItem.classList.add('grid-item');
			}

			if (m == 'p') {
				create = document.createElement('p');
				create.textContent = g.para;
			}
			gridItem.classList.add('grid-item');
			gridItem.appendChild(create);
			grid.classList.add('grid');
			grid.appendChild(gridItem);
			cont.appendChild(grid);
		});
	});
}

```

***

</br>
</br>

Code -home.js- :

```javascript 

import Home from "./home.js";
import Contact from "./contact.js";
import Menu from "./menu.js";

const Homebtn = document.getElementById("Home"),
      Menubtn = document.getElementById("Menu"),
      Contactbtn = document.getElementById("Contact"),
      cont = document.getElementById('content');

Home();

```

***

</br>
</br>

Code -style.css- :

```css
:root{
    --navBck : #ffd54ddc;
    --contBck : rgba(204, 146, 155, 0.549) ;
    --body : rgb(47, 182, 47);
    --background-light: rgba(170, 170, 170, 0.874);
    --border-color: #222; 
    --menu-grid:   rgba(107, 107, 107, 0.945);
    --menu-g-item: rgba(170, 170, 170, 0.938);
    --btn: rgb(245, 87, 92); 
    --txt: rgb(230, 102, 102);
    --form: rgba(204, 146, 155, 0.57); 
}

@font-face{
    font-family: 'Home-p';
    src: url(../dist/Oswald-VariableFont_wght.ttf) ;
    font-size: 1vw;
    font-weight: 500 ;
}
@font-face {
    font-family: 'grid-p';
    src: url(../dist/Oswald-VariableFont_wght.ttf);  
}

@font-face {
    font-family: 'footer';
    src: url(../dist/SansitaSwashed-VariableFont_wght.ttf);
    font-size: 2vw;
    font-weight: 600;
}

*,
*::after,
*::before{
    margin: 0;
    padding: 0;
}

body{
    display:block;
}

  
nav{
    display: flex;
    background-color: var(--navBck);
    width: 70vw;
    height: 100px;
    align-items: center;
    justify-self: center;
    margin-top: 2vw;
    border-radius: 0 10% 20% 40% ;
}
nav > ul {
    display: flex;
    /* padding: 2vw; */
    list-style: inside;
}
.button-nav{
    padding: 1vw;
    cursor: pointer;
    margin-left: 2vw;
    /* border: 2px solid black; */
    border-radius: 20%;
    font-family: 'Home-p';
    font-size: 2vw; 
}
.button-nav:hover {
    animation: navColor 1s linear ; 
} 
img[alt*=logo]{
    /* opacity: 0.8; */
    cursor: pointer;
    border-radius: 5%;
    width : 10vw;
    height: 10vw;
    margin-bottom: -2vw;
    margin-left: 5px;
}
img[alt*=logo]:hover{
    /* animation: zoom-in 1s alternate 2 ease-in; */
    transform: scale(1.5,1.5);
    transition-duration: 1s;
}

a{
    text-decoration: none;
    color: #222;
}



 /*  Home style */
 .home{
    /* background-image: url(./img/table-top-with-background.jpg); */
    background-image: url(../src/img/table-top-with-background.png);
    background-size: cover;
    width: 95vw;
    height: 95vh;
    opacity: 0.9;
    
}
.content{
    margin: 2vw;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 7vw ;
    
}
.home-img{
    width: 20vw;
    height: 20vw;
    border-radius: 5%;
    box-shadow:  10px 10px 10px 0 rgba(0,0,0,0.19) ;
    border: 5px solid  var(--contBck) ;
}

.home-p{
    font-family: 'Home-p';
    width: 40ch;
    background-color: var(--contBck);
    padding: 2vw;
    border-radius: 20% 0 0 0 ;
}
/* ********************************************* */



/* Menu Style */
    .menu{
    background-image: url(../src/img/Background1.png);
    background-size: cover;  
    width: 100vw;
    height: 90vh;
    opacity: 0.9;
    }
   
    .grid{
        display: grid;
        justify-content: center;
        align-items: center;
        background-color: var(--menu-grid);
        margin: 5vw 5vw ;
        width: 60vw;
        gap: 1vw;
        padding: 1vw;
        /* opacity: 0.5; */
    }
    .grid-item{
        background-color: var(--menu-g-item);
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center; 
        padding: 1.5vw;
        font-family: 'grid-p';
        font-size: 3vw;
        text-align: center;
        cursor: pointer;
    }
    .grid-item:hover{
        background-color: rgba(138, 131, 131, 0.874);
    }
    strong{
        font-weight: 800;
    }
   .grid-item img{
        width: 20vw;
        height: 20vw;
        opacity: 1;
        padding: 1vw;
        border-radius: 10%;
    }
    .grid-item img:hover{
        transform: scale(1.1,1.1);
        transition-duration: 1s;
    }
/* ********************************************* */

/* Contact Style */
    .contact{
        /* background-image: url(../src/img/table-top-with-background.png); */
        background-size: cover;
        /* background-repeat: no-repeat; */
        width: 100vw;
        height: 100vh;
    }
    form{
        display: flex;
        flex-direction: column;
        margin: 5vw;
        align-items: center;
        justify-content: center;
        font-family: 'home-p';
        padding: 2vw;
    }
    fieldset{
        display: flex;
        flex-direction: column;
        padding: 2vw;
        width: 30vw;
        height: 30vh;
        background-color: var(--form);
    }
    label{
        margin-top: 1vw;
    }
    textarea{
        width: 80%;
        height: 70%;
        padding: 1vw;
        font-family: 'grid-p';
        max-width: 30vw;
    }
    input[type*=email]{
        width: 80%;
        font-family: 'grid-p';
    }
    input[type*=submit]{
        background-color: var(--btn);
        border: none;
        border-radius: 5px;
        padding: 2vw;
        margin-top: 2vw;
        margin-bottom: 2vw;
        cursor: pointer;
        width: 10vw;
    }
    textarea:valid{
        background-color:rgb(127, 196, 100);
    }
    textarea:invalid{
        background-color: rgb(230, 102, 102);
    }
    input:valid {
        border-color: rgb(127, 196, 100);
    }
    input:invalid {
        border-color: rgb(230, 102, 102);
    }
    .control {
        box-shadow: none;
        background-color: rgba(0, 0, 0, 0.02);
        border-radius: 0px;
        border-color: #ccc;
        border-style: none none solid none;
        transition: all 0.5s;
    }
    .control::placeholder {
        color: transparent;
    }
    .control:focus {
        box-shadow: none;
        outline: none;
    }
    .control:focus + .label,
    .control:not(:placeholder-shown) + .label {
        transform: translate(-1em) scale(0.8);
    }
    
/* ********************************************* */

/* Footer */

footer {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    position: fixed;
    left: 0;
    bottom: 0;
    width:100vw;
    padding: 1vw;
    border-top: 1px solid var(--border-color);
    background-color: var(--background-light);
    font-family: 'footer';
  }
 
  .fa-github:hover {
    cursor: pointer;  }
  .fa-twitter:hover {
    cursor: pointer;
  }
/* ******************************************** */


@media screen and (max-width : 700px) {
   
   /* Home  */

    .home-img{
        width: 40vw;
        height: 40vw;
    }
    .home-p{
        font-size: smaller;
        width: 30ch;
    }
    nav{
        height: 8vw;
    }
    nav > ul > li {
        font-size: x-small;
    }
    img[alt*=logo]{
        width : 10vw;
        height: 10vw; 
    }

    /* Menu */

    .grid{
        grid-template-columns: repeat(1,1fr);
    }
    .grid-item img{
        width: 15vw;
        height: 15vw;
        justify-content: center;
    }
    fieldset{
        height: 30vw;
    }
    footer{
        font-size: 3vw;
    }
}

@keyframes zoom-in {
    from{transform: scale(1,1);}
    to{transform: scale(1.5,1.5);}
}

@keyframes navColor {
    from{background-color: var(--navBck);}
    to{ background-color: var(--contBck) ;}
}

```

***

</br>
</br>

Code -index.html- :

```html 

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="../src/style.css">
    <link rel="shortcut icon" href="../src/img/Mashawi.jpg" />
    <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"
  />
    <title>Restaurant</title>
</head>
<body>
    <header>
        <nav>
            <img src="../src/img/my—logo—.png" alt="logo">
            <ul>
                <li id="Home" class="button-nav">
                    Home
                </li>
                <li id="Menu" class="button-nav">
                    Menu
                </li>
                <li id="Contact" class="button-nav">
                    Contact
                </li>
            </ul>
        </nav>
    </header>

    <div id="content" class="content"></div>




    <footer class="footer">
        <p>
          Copyright © 
          <script>
            document.write(new Date().getFullYear())
          </script>
           Omar-Alzant
        </p>
        <a href="https://github.com/omar-alzant" target="_blank">
          <i class="fa fa-github"></i></a>
        <a href="https://twitter.com/OjZ2297" target="_blank">
            <i class="fa fa-twitter"></i>
        </a>
      </footer>
      <script type="module" src="../src/index.js"></script>
      <!-- <script type="module" src="main.js"></script> -->

</body>
</html>

```