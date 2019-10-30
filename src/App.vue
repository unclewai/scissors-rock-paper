<template>
  <div id="app">
    <div id="bot-placeholder">
      <img :src="bot_image">
    </div>
    <div id="you-placeholder">
      <img :src="you_image">
    </div>
    <div id="buttons-container">
      <div id="btn-paper" @click="() => userPicked(1)"></div>
      <div id="btn-scissor" @click="() => userPicked(2)"></div>
      <div id="btn-rock" @click="() => userPicked(3)"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      botChoice: 0,
      userChoice: 0,
    }
  },
  computed: {
    bot_image() {
      let botChoices = {};
      botChoices['-30'] = 'rock-lose.png';
      botChoices['-20'] = 'scissor-lose.png';
      botChoices['-10'] = 'paper-lose.png';
      botChoices['0'] = 'Placeholder-Bot.png';
      botChoices['10'] = 'paper-win.png';
      botChoices['20'] = 'scissor-win.png';
      botChoices['30'] = 'rock-win.png';
      botChoices['101'] = 'paper-draw.png';
      botChoices['102'] = 'scissor-draw.png';
      botChoices['103'] = 'rock-draw.png';

      return `/images/${botChoices[this.botChoice]}`
    },
    you_image() {
      let userChoices = {};
      userChoices['-30'] = 'rock-lose.png';
      userChoices['-20'] = 'scissor-lose.png';
      userChoices['-10'] = 'paper-lose.png';
      userChoices['0'] = 'Placeholder-Bot.png';
      userChoices['10'] = 'paper-win.png';
      userChoices['20'] = 'scissor-win.png';
      userChoices['30'] = 'rock-win.png';
      userChoices['101'] = 'paper-draw.png';
      userChoices['102'] = 'scissor-draw.png';
      userChoices['103'] = 'rock-draw.png';

      return `/images/${userChoices[this.userChoice]}`
    }
  },  
  methods: {
      userPicked(userPicked) {
        let botPicked = Math.floor(Math.random() * 3) + 1;
        
        /* eslint-disable no-console */
        console.log(userPicked);
        console.log(botPicked);
        /* eslint-enable no-console */

        
        if ( userPicked == botPicked ) {
          this.botChoice = botPicked + 100;
          this.userChoice = userPicked + 100;
        } else if ( userPicked == 1 && botPicked == 3 || userPicked == 2 && botPicked == 1 || userPicked == 3 && botPicked == 2 ) {
          this.botChoice = botPicked * -10;
          this.userChoice = userPicked * 10;
        } else if ( userPicked == 1 && botPicked == 2 || userPicked == 2 && botPicked == 3 || userPicked == 3 && botPicked == 1 ) {
          this.botChoice = botPicked * 10;
          this.userChoice = userPicked * -10;
        }

      }
    }  
}
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  background-color: #44D7B6;
  padding-top: 40px;
  box-sizing: border-box;
}

#bot-placeholder, #you-placeholder {
  flex: 0px 2 1;
}

#bot-placeholder img, #you-placeholder img {
  display: block;
  width: 60%;
  height: auto;
  margin: auto;
}

#buttons-container {
  flex: 0px 1 1;
  display: flex;
  flex-direction: row;
}

#buttons-container div {
  flex: 0px 1 1;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center bottom;
}

#buttons-container div#btn-paper {
  background-image: url('/images/paper-btn.png');
}

#buttons-container div#btn-scissor {
  background-image: url('/images/scissor-btn.png');
}

#buttons-container div#btn-rock {
  background-image: url('/images/rock-btn.png');
}
</style>