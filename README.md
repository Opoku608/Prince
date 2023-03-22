<!DOCTYPE html>
<html>
<head>
<style id="default-theme">
		.card-container {
			display: flex;
			flex-wrap: nowrap;
			overflow-x: auto;
			scroll-snap-type: x mandatory;
			-webkit-overflow-scrolling: touch;
			padding: 10px;
		}
		.card {
			width: 300px;
			flex-shrink: 0;
			margin-right: 10px;
			background-color: #f6f6f6;
			border: 1px solid #ddd;
			padding: 20px;
			scroll-snap-align: center;
			text-align: center;
			transition: all 0.5s ease-out;
			cursor: pointer;
			position: relative;
		}
		.card:before {
			content: "";
			position: absolute;
			top: 0;
			left: 0;
			width: 100%;
			height: 100%;
			background-image: linear-gradient(to bottom right, #bde5fc, #fff);
			opacity: 0.5;
			z-index: -1;
			transform: scaleX(-1);
			transition: all 0.5s ease-out;
		}
		.card:hover:before {
			opacity: 0.8;
		}
		.card:hover {
			transform: scale(1.1);
		}
		.card h1 {
			margin-top: 0;
		}
		.card p {
			margin-bottom: 0;
		}
		a {
		  text-decoration: none;
		  color: black;
		}

#myInput {
  background-position: 5px 10px;
  background-size:40px;
  background-repeat: no-repeat;
  width: 100%;
  box-sizing: border-box;
  font-size: 16px;
  padding: 12px 20px 12px 40px;
  border: 1px solid #ddd;
  margin-bottom: 12px;
}


#myTable {
  border-collapse: collapse;
  width: 100%;
  border: 1px solid #ddd;
  font-size: 18px;
}


#myTable th, #myTable td {
  text-align: left;
  padding: 12px;
}


#myTable tr {
  border-bottom: 1px solid #ddd;
}

 #myTable tr:hover{
  background-color: #f1f1f1;
}
tr.header{
  background-color: #7B7B7B;
}
#bar{
  width: calc(100vw - 5px);
  background-color: #B0B0B0;
}
#barEnd {
  width: calc(100vw - 1px);
  background-color: #B0B0B0;
 max-height: 100px;
}
#logo {
  border-radius: 100%;
}
</style>

    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>

<body>
<table id="bar">
  <tr>
    <td><b><font size="1">Muslim Plateform </font></font></td>
    <td><font size="5"><b>Qalam</b> </font></td>
    <td><img srcset="LOGO loading" src="https://qalam-islam.000webhostapp.com/Images/Logo.png" alt="Loading Logo" height="50px" align="right" id="logo"></td>
  </tr>
</table>

<h1>Top articles</h1>
<div>
  <label>Sort by:</label>
  <select id="sort-select">
    <option value="popularity">Popularity</option>
    <option value="newest">Newest</option>
    <option value="a-z">A-Z</option>
  </select>
</div>
<div class="card-container">
</div>  


<script>
  const cardContainer = document.querySelector('.card-container');
  
  function fetchData(url) {
    return fetch(url)
      .then(response => response.text())
      .then(text => text.split('\n').filter(item => item.trim() !== ''));
  }
  
  function sortCards(sortBy) {
    const cards = [...cardContainer.children];
    switch (sortBy) {
      case 'popularity':
        cards.sort((a, b) => b.innerText - a.innerText);
        break;
      case 'newest':
        cards.sort((a, b) => new Date(b.dataset.date) - new Date(a.dataset.date));
        break;
      case 'a-z':
        cards.sort((a, b) => a.innerText.localeCompare(b.innerText));
        break;
    }
    cards.forEach(card => cardContainer.appendChild(card));
  }
  fetchData('https://qalam-islam.000webhostapp.com/Data/article.txt')
    .then(
      articles => {
      articles.forEach((article, index) => {
        const card = document.createElement('div');
        card.classList.add('card');
        card.innerText = index + 1 + '. '+article;
        card.dataset.date = new Date().toISOString();
        cardContainer.appendChild(card);
      });
      const sortSelect = document.querySelector('#sort-select');
      sortSelect.addEventListener('change', () => {
        sortCards(sortSelect.value);
      });
      sortCards(sortSelect.value);
    });
  
</script>


<input type="text" id="myInput"
onkeyup="myFunction()" placeholder=
"Search by Options Title or Discription...."

title="Type in a name">
	<div class="card-container">
	 
<table id="myTable">
<tr class="header">
<th>Options</th>
</tr>
  <tr>
    <td>
    	<a href scr="#">  <div class="card">
    <h1>Islamic Topics</h1>
    <p>All from Halal and haram to Prayers </p>
        </td>
        </div></a>
  </tr>

  <tr>
    <td>
   	<a href scr="#">   <div class="card">
    <h1>About</h1>
    <p>What this plateform is about and mission of it.</p>
     </div></a>
    </td>
  </tr>

  <tr>
    <td>
   	<a href scr="#">   <div class="card">
    <h1>Crdits</h1>
    <p>Crdits of all who have entered or jumped out of the project </p>
     </div></a>
    </td>
  </tr>

     <td>
   	<a>   <div class="card">
    <h1>Custom theme</h1>
    <p>edit the theme of Website </p>
    
    <label for="colorInput">Choose a color:</label>
    <br>
    <br> 
    <input type="color" id="colorInput" oninput="addtheme()">
    <h3 id="default" onclick="defaultTheme()">Tap me for resetting to default </h3>
     </div></a>
    </td>
  </tr>
 
</table>
</div>
   <table id="barEnd">
     <tr>
       <td><b>More options will come in future </b></td>
     </tr>
  <tr>
    <td><b><font size="1">Qalam </font></font></td>
    <td><font size="1"><b>Home page</b> </font></td>
    <td>rights ® of Qalam</td>
  </tr>
  
   </table>
<script>

function myFunction() {
var input, filter, table, tr, td, i;
input=document.getElementById("myInput");

filter=input.value.toUpperCase();

table=document.getElementById("myTable");

tr=table.getElementsByTagName("tr");

for (i = 0; i < tr.length; i++) {
// td = tr[i].getElementsByTagName("td")[1];
td = td = tr[i].getElementsByTagName("td")[0]; //+  tr[i].getElementsByTagName("td")[1];
 if (td) {
   if (td.innerHTML.toUpperCase()
   .indexOf(filter) > -1) {

     tr[i].style.display = "";
      } else {
        tr[i].style.display = "none";

      }
    }
   
  }
  
}

// Custom Theme code
//select theme
function addtheme(){
  applyCSS(generateTheme(document.getElementById('colorInput').value))
  localStorage.setItem('Qalam-CustomTheme',document.getElementById('colorInput').value)   
  console.log('working')
}
//Default theme
function defaultTheme(){
  localStorage.removeItem('Qalam-CustomTheme')
    location.reload(true);
}



// Add theme 
var ThemeColor = localStorage.getItem('Qalam-CustomTheme')
if (!ThemeColor){
  ThemeColor = NaN
}else if(ThemeColor){
  applyCSS(generateTheme(ThemeColor))
}else{
  alert('Error - You may tell Devlopers '+Error("Unknown Color can't define please check broswer"))
  
}
//Function library 
  function generateTheme(color) { 
     let cssCode = `
    .card-container {
  display: flex;
  flex-wrap: nowrap;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
  padding: 10px;
}

.card {
  width: 300px;
  flex-shrink: 0;
  margin-right: 10px;
  background-color: ${shadeColor("#f6f6f6", -10)};
  border: 1px solid ${shadeColor("#f6f6f6", -20)};
  padding: 20px;
  scroll-snap-align: center;
  text-align: center;
  transition: all 0.5s ease-out;
  cursor: pointer;
  position: relative;
}

.card:before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: linear-gradient(to bottom right, ${shadeColor("#bde5fc", -10)}, #fff);
  opacity: 0.5;
  z-index: -1;
  transform: scaleX(-1);
  transition: all 0.5s ease-out;
}

.card:hover:before {
  opacity: 0.8;
}

.card:hover {
  transform: scale(1.1);
}

.card h1 {
  margin-top: 0;
}

.card p {
  margin-bottom: 0;
}

a {
  text-decoration: none;
  color: black;
}

#myInput {
  background-position: 5px 10px;
  background-size:40px;
  background-repeat: no-repeat;
  width: 100%;
  box-sizing: border-box;
  font-size: 16px;
  padding: 12px 20px 12px 40px;
  border: 1px solid #ddd;
  margin-bottom: 12px;
}

#myTable {
  border-collapse: collapse;
  width: 100%;
  border: 1px solid #ddd;
  font-size: 18px;
}

#myTable th, #myTable td {
  text-align: left;
  padding: 12px;
}

#myTable tr {
  border-bottom: 1px solid #ddd;
}

#myTable tr:hover{
  background-colo
