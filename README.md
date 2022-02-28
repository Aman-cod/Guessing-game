# Guessing-game
 its guessing game where you will guess a number and it will give if it is correct or not and this game is made using html,css and javascript
 //html file
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="C:\Users\KIIT\OneDrive\Desktop\Building Game Using JAVASCRIPT\stylw.css" />
    <title>Document</title>
  </head>
  <body onload="init()">
    <main>
      <div id="welcomeScreen">
        <h2>Guess The Random Number Between 1-100</h2>
        <img class="image" src="game_logo.png" alt="logo" />

        <section class="eventSection">
          <p>Select The Difficulty</p>
          <div class="button-wrapper">
            <button onclick="easyMode()">Easy: 10 attempts</button>
            <button onclick="hardMode()">Hard: 5 attempts</button>
          </div>
        </section>
      </div>
      <!-- our acual game area  -->
      <div id="gameArea">
        <div id="newGameButton">
          <button onclick="newGameBegin()">New Game</button>
        </div>

        <section>
          <h3 id="textOutput">Your Guess</h3>
          <input
            type="number"
            id="inputBox"
            min="1"
            max="100"
            placeholder="Enter Your Number"
            onchange="compareGuess()"
          />
        </section>

        <section class="stats">
          <div class="info">
            <p>Number of previous attempts</p>
            <span id="attempts"> 0 </span>
          </div>
          <div class="info">
            <p>Number of previous guesses</p>
            <span id="guesses"> 0 </span>
          </div>
        </section>
      </div>
    </main>
    <script src="C:\Users\KIIT\OneDrive\Desktop\Building Game Using JAVASCRIPT\indes.js"></script>
  </body>
</html>
//css file
 @import url("https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@300;400&family=Montserrat:wght@600&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  --dark: #350363;
  --background: #ffe9db;
}

html {
  font-size: 62.5%;
  font-family: "Montserrat", sans-serif;
}

body {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: auto;
  background-color: #491579;
}

main {
  width: 30vw;
  text-align: center;
  background-color: var(--background);
  border: solid var(--dark);
  border-width: 0.8rem;
  border-radius: 1rem;
  padding: 8rem 5rem;
  color: #1f2933;
}

h2 {
  font-size: 2.2rem;
  margin: 2rem;
}

h3 {
  font-size: 3rem;
}

p {
  font-size: 1.8rem;
}

.image {
  width: 90%;
  max-height: 22rem;
  height: auto;
  margin: 1rem 0 4rem 0;
}

.button-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-bottom: 4rem;
  margin-bottom: 2rem;
}

button {
  min-width: 28rem;
  background-image: linear-gradient(
    92.88deg,
    #455eb5 9.16%,
    #5643cc 43.89%,
    #673fd7 64.72%
  );
  border-radius: 0.8rem;
  border-style: none;
  color: #ffffff;
  cursor: pointer;
  padding: 2.5rem 6rem;
  font-size: 2rem;
  text-align: center;
  margin-bottom: 2rem;
  text-shadow: rgba(0, 0, 0, 0.25) 0 3px 8px;
  transition: all 0.5s;
  user-select: none;
  -webkit-user-select: none;
  text-transform: capitalize;
  font-family: "Josefin Sans", sans-serif;
}

button:hover {
  box-shadow: rgba(80, 63, 205, 0.2) 0 1px 30px;
  transition-duration: 0.1s;
}

button:last-child {
  background: var(--dark);
  margin-bottom: 0;
}


/*-------------------------------
 our game area   
 ---------------------------------*/

#gameArea {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

#newGameButton button {
  margin: 2rem 0;
}

input {
  border: 0.1rem solid lightgray;
  background: transparent;
  margin: 4rem 0;
  padding: 2rem 0;
  width: 25rem;
  text-align: center;
  font-family: "Josefin Sans", sans-serif;
}

.stats {
  text-align: left;
  margin-bottom: 4rem;
}

.info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 3rem;
}

.info span {
  font-size: 2rem;
  color: #ff0511;
}

/*-------------------------------
 for responsive  
 ---------------------------------*/
 @media (max-width: 1200px) {
    body {
      width: 100vw;
    }
    main {
      width: 50vw;
      padding: 2rem;
    }
    input {
      width: 20rem;
    }
  }
  
  @media (max-width: 800px) {
    body {
      width: 100vw;
    }
    main {
      width: 80vw;
      padding: 2rem;
    }
  
    #welcomeScreen h2 {
      text-transform: capitalize;
      font-size: 2rem;
    }
  
    button {
      min-width: 20rem;
    }
    .button-wrapper button {
      font-size: 1.5rem;
    }
    input {
      width: 20rem;
    }
  
    .info {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: space-between;
    }
    .info span {
      margin-top: 1rem;
      font-size: 1.6rem;
    }
  }
  //js file
  let computerGuess;
let userGuess = [];
let userGuessUpdate = document.getElementById("textOutput");
let userNumberUpdate = document.getElementById("inputBox");
let audio = new Audio("/mixkit-arcade-mechanical-bling-210.mp3");

const init = () => {
  computerGuess = Math.floor(Math.random() * 100);
  ////console.log(computerGuess);
  document.getElementById("newGameButton").style.display = "none";
  document.getElementById("gameArea").style.display = "none";
};

const startGame = () => {
  document.getElementById("welcomeScreen").style.display = "none";
  document.getElementById("gameArea").style.display = "block";
};

// relaod the page

const newGameBegin = () => {
  window.focus();
  audio.play();
  window.location.reload();
};

// start new game

const startNewGame = () => {
  document.getElementById("newGameButton").style.display = "inline";
  userNumberUpdate.setAttribute("disabled", true);
}; 
// main logic of our app
const compareGuess = () => {
    audio.play();
    const userNumber = Number(document.getElementById("inputBox").value);
    userGuess = [...userGuess, userNumber];
    document.getElementById("guesses").innerHTML = userGuess;
  
    // check the value low or high
  
    if (userGuess.length < maxGuess) {
      if (userNumber > computerGuess) {
        userGuessUpdate.innerHTML = "Your guess is High 😲";
        userNumberUpdate.value = "";
      } else if (userNumber < computerGuess) {
        userGuessUpdate.innerHTML = "Your guess is Low 😌";
        userNumberUpdate.value = "";
      } else {
        userGuessUpdate.innerHTML = "It's Correct 😀";
        userNumberUpdate.value = "";
        startNewGame();
      }
    } else {
      if (userNumber > computerGuess) {
        userGuessUpdate.innerHTML = `You Loose!! correct number was ${computerGuess}`;
        userNumberUpdate.value = "";
        startNewGame();
      } else if (userNumber < computerGuess) {
        userGuessUpdate.innerHTML = `You Loose!! correct number was ${computerGuess}`;
        userNumberUpdate.value = "";
        startNewGame();
      } else {
        userGuessUpdate.innerHTML = "It's Correct 😀";
        userNumberUpdate.value = "";
        startNewGame();
      }
    }
  
    document.getElementById("attempts").innerHTML = userGuess.length;
  };
  
  const easyMode = () => {
    audio.play();
    maxGuess = 10;
    startGame();
  };
  
  const hardMode = () => {
    audio.play();
    maxGuess = 5;
    startGame();
  }; 
