<script>

// import Hexagon from './Hexagon.vue';
import { questions } from '../data/q&a';

export default {
  name: "Main",
  components: {
    // Hexagon
  },
  created() {},
  data() {
    return {
      questions,
      randomNum:'',
      usedNum:[],
      message:''
    }
  },
  props: {},
  methods: {
  
  randomizer() {
    // Genera un numero casuale compreso tra 0 e il numero di domande meno uno
    this.randomNum = Math.floor(Math.random() * this.questions.length);

    // Verifica se il numero generato è già stato utilizzato
    if (!this.usedNum.includes(this.randomNum)) {
      // Se il numero casuale non è stato utilizzato, restituisci true
      return true;
    } else {
      // Se il numero casuale è già stato utilizzato, restituisci false
      return false;
    }
  },
  nextQuestion() {
  // Rimuovi la classe "active" da tutti gli elementi di risposta
  this.message = '';
  for (let i = 0; i < 4; i++) {
    document.getElementById('answer' + i).classList.remove('active');
    document.getElementById('answer' + i).classList.remove('wrong-answer');
    document.getElementById('answer' + i).classList.remove('correct-answer');
  }

  // Chiamata alla funzione randomizer per ottenere un numero casuale
  while (!this.randomizer()) {
    // Continua a generare un nuovo numero finché non è uno non utilizzato
  }

  // Una volta ottenuto un numero casuale non utilizzato, lo aggiungi all'array usedNum
  this.usedNum.push(this.randomNum);

  console.log(this.randomNum);
  console.log('Answer: ' + questions[this.randomNum]?.correct);
},
  selectedAnswer(id) {
    // Qui catturiamo l'id della risposta selezionata e lo passiamoa verifyAnswer
    // this.verifyAnswer(id);
    document.getElementById('answer'+id).classList.toggle('active');
  },
  verifyAnswer() {
    // Aggiungi qui la logica per verificare la risposta
    // Qui devi ottenere l'id della risposta selezionata e passarlo a verifyAnswer
    const selectedAnswerId = document.querySelector('.hexagon.active').id.slice(-1); // Ottieni l'id dell'elemento attivo
    const correctAnswerId = this.questions[this.randomNum].correct;
    console.log('selectedAnswerId: '+selectedAnswerId);
    console.log('correctAnswerId: '+correctAnswerId);
    if (selectedAnswerId == correctAnswerId) {
      this.message = 'Correct!'
      document.getElementById('answer'+selectedAnswerId).classList.remove('active');
      document.getElementById('answer'+selectedAnswerId).classList.add('correct-answer');
      console.log('Risposta corretta!');
   
    } else {
    
      document.getElementById('answer'+selectedAnswerId).classList.remove('active');
      document.getElementById('answer'+selectedAnswerId).classList.add('wrong-answer');
      document.getElementById('answer'+correctAnswerId).classList.toggle('correct-answer');
      this.message = 'Wrong answer!'
      console.log('Risposta sbagliata!');
    }
  }
}

}
</script>

<template>
  <main>
    <div class="container-custom">
      <div class="hexagon question">{{ questions[this.randomNum]?.question }}</div>
      <div class="grid-container">
        <div @click="selectedAnswer(0)" id="answer0" class="hexagon answer"> 
          <h5 class="perma-letter">A.</h5>
          <p>{{ questions[this.randomNum]?.content[0] }}</p>
        </div>
        <div @click="selectedAnswer(1)" id="answer1" class="hexagon answer">
          <h5 class="perma-letter">B.</h5>
          <p>{{ questions[this.randomNum]?.content[1] }}</p>
        </div>
        <div @click="selectedAnswer(2)" id="answer2" class="hexagon answer">
          <h5 class="perma-letter">C.</h5>
          <p>{{ questions[this.randomNum]?.content[2] }}</p>
        </div>
        <div @click="selectedAnswer(3)" id="answer3" class="hexagon answer">
          <h5 class="perma-letter">D.</h5>
          <p>{{ questions[this.randomNum]?.content[3] }}</p>
        </div>
      </div>
      <div id="message">
        <h3>{{ this.message }}</h3>
      </div>
      <div class="btn-container">
        <div @click="verifyAnswer()" class="btn btn-verify">VERIFY</div>
        <div @click="nextQuestion()" class="btn btn-next">NEXT QUESTION</div>
      </div>
    </div>
  </main>
</template>


<style lang="scss" scoped>
.container-custom {
  width: 95%;
  color: white;
  margin: 0 auto;
  padding-top: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  .question {
    width: 1500px;
   
  }
  #message {
    height: 20px;
  }
}
.hexagon {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 60px;
  line-height: 100%;
  color: white;
  border: 2px solid white;
  border-radius: 10px;
  overflow: auto;
  position: relative;
  .perma-letter {
    margin-right: 20px;
    position: absolute;
    left: 20px;
  }
}
.grid-container  {
  width: 100%;
  padding-top: 50px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  
 
  .answer {
    flex-basis: 49.5%;
    cursor: pointer;
    margin-bottom: 20px;
    &.active {
      color: #11093A;
    }
    
  }
}
.btn-container {
  width: 100%;
  margin-top: 100px;
  display: flex;
  justify-content: flex-end;
  .btn-verify,
  .btn-next {
    margin-right: 10px;
    color: white;
    border: 2px solid white;
  }
  .btn-verify:hover {
    background-color: green;
  }
  .btn-next:hover {
    background-color: #171B86;
  }
}
</style>