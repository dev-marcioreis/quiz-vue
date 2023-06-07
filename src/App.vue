<script setup>

  import { ref, computed } from 'vue';
  
  const questions = ref([
    {
      question: 'Quem descobriu o Brasil?',
      answer: 0,
      options: [
        'Pedro Alvares Cabral',
        'Pedro Alves',
        'Pedro Cabralia'
      ],
      selected: null
    },
    {
      question: 'Em que ano o Brasil foi descoberto?',
      answer: 2,
      options: [
        '2023',
        '1350',
        '1500'
      ],
      selected: null
    },
    {
      question: 'Qual a capital do Brasil?',
      answer: 1,
      options: [
        'Bragança',
        'Brasília',
        'Belém'
      ],
      selected: null
    }
  ]);

  const completedQuiz = ref(false)
  const currenteQuestion = ref(0)

  const scoreQuiz = computed(() => {

    let value = 0

    questions.value.map(quest => {
      
      if(quest.selected == quest.answer) {
        value++
      }
    })
    return value

  });

  const getCurrentQuestion = computed(() => {

    let question = questions.value[currenteQuestion.value]
    question.index = currenteQuestion.value

    return question

  });

  const setAnswer = eAnswer => {

    questions.value[currenteQuestion.value].selected = eAnswer.target.value
    eAnswer.target.value = null

  };

  const nextQuestion = () => {

    if(currenteQuestion.value < questions.value.length - 1) {
      currenteQuestion.value++
    } else {
      completedQuiz.value = true
    }

  };

  const reloadPage = () => {
    window.location.reload()
  }

</script>
  
<template>

  <main class="main container">
    <h1>quiz<span>vue</span></h1>

    <section class="quiz-container" v-if="!completedQuiz">

      <div class="quiz-info">
        <p class="question">{{ getCurrentQuestion.question }}</p>
        <p class="score">resposta: <span>{{ scoreQuiz }}/{{ questions.length }}</span></p>
      </div>

      <div class="options">
        <label v-for="(option, index) in getCurrentQuestion.options" 
        :key="index" 
        :class="`option ${getCurrentQuestion.selected == index 
          ? index == getCurrentQuestion.answer 
          ? 'correct' : 'wrong' : ''}
          ${getCurrentQuestion.selected != null && index != getCurrentQuestion.selected 
          ? 'disable' : ''}`">

          <input 
            type="radio" 
            :name="getCurrentQuestion.index" 
            :value="index" 
            v-model="getCurrentQuestion.selected"
            :disabled="getCurrentQuestion.selected"
            @change="setAnswer"
          >

          <span>{{ option }}</span>

          </label>
      </div>

      <button @click="nextQuestion" :disabled="!getCurrentQuestion.selected">
        {{ 
          getCurrentQuestion.index == questions.length - 1 
          ? 'Finalizar' : getCurrentQuestion.selected == null 
          ? 'Selecione uma opção' : 'Próxima pegunta'
        }}
      </button>

    </section>

    <section v-else class="finish">
      <h2>Você terminou o quiz!</h2>
      <p>Seus acertos: <span>{{ scoreQuiz }} / {{ questions.length }}</span></p>
      <button class="reload" @click="reloadPage()">começar denovo</button>
    </section>

  </main>

</template>

<style lang="css">

  /*==========Reset==========*/
  *, *::before, *::after {
        margin: 0;
        padding: 0;
        border: 0;
        box-sizing: border-box;
        outline: none;
        text-decoration: none;
        list-style: none;
        font-family: 'Poppins', sans-serif;
    }

  /*==========Base==========*/
  :root {

    --primary-color: hsl(25, 76%, 90%);
    --dark-color: hsl(0, 0%, 13%);
    --white-color: hsl(0, 0%, 100%);
    --green-color: hsl(154, 49%, 49%);
    --red-color: hsl(347, 100%, 71%);

    --transition: all 400ms ease-in-out;
    --shadow: 0px 1px 3px hsla(0, 0%, 0%, 0.5);
    --shadow-1: 0px 3px 6px hsla(0, 0%, 0%, 0.4);

    --container-lg: 80%;
    --container-md: 90%;
    --container-max-wd: 1800px;

  }

  /*==========Base==========*/
  body {
    background: var(--primary-color);
    color: var(--dark-color);
  }

  ::-webkit-scrollbar {
    width: .5rem;
  }
  ::-webkit-scrollbar-track {
    background: var(--dark-color);
  }
  ::-webkit-scrollbar-thumb {
    background: var(--primary-color);
  }
  .container {
    width: var(--container-lg);
    max-width: var(--container-max-wd);
    margin-inline: auto;  
  }

  /*==========Quiz==========*/
  .main {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    min-height: 100vh;
  }
  .main h1 {
    margin-block-end: 1rem;
    text-transform: uppercase;
    text-shadow: var(--shadow-1);
    color: var(--white-color);
    font-size: 2.5rem;
    letter-spacing: 2px;
  }
  .main h1 span {
    font-size: 1.1rem;
    font-weight: 600;
    color: var(--green-color);
    text-shadow: none;
    margin-left: .3rem;
    font-style: italic;
  }
  .quiz-container {
    width: 100%;
    max-width: 640px;
    background: var(--white-color);
    padding: 1rem;
    border-radius: .5rem;
    box-shadow: var(--shadow);
  }
  .quiz-info {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-block-end: 2rem;
  }
  .quiz-info .question {
    font-size: 1.5rem;
    font-weight: 400;
  }
  .quiz-info .score {
    text-transform: uppercase;
    font-weight: 400;
  }
  .quiz-info .score span {
    color: var(--red-color);
    font-weight: 500;
  }
  .options {
    margin-block-end: 2rem;
  }
  .options .option {
    display: block;
    padding: .5rem;
    cursor: pointer;
    transition: var(--transition);
  }
  .options .option:hover {
    background: hsl(0, 0%, 91%);
  }
  .option.correct {
    background: var(--green-color);
    color: var(--white-color);
  }
  .option.wrong {
    background: var(--red-color);
    color: var(--white-color);
  }
  .option:last-of-type {
    margin-block-end: 0;
  }
  .option.disable {
    opacity: 0.5;
  }
  .option input {
    display: none;
  }
  button {
    appearance: none;
    padding: .5rem 1rem;
    cursor: pointer;
    background: var(--dark-color);
    color: var(--white-color);
    box-shadow: var(--shadow);
  }
  button:disabled {
    opacity: 0.5;
  }
  .finish {
    background: var(--white-color);
    padding: 1rem;
    border-radius: .5rem;
    box-shadow: var(--shadow);
    text-align: center;
  }
  .finish h2 {
    color: var(--green-color);
    font-weight: 500;
    margin-block-end: 1rem;
  }
  .finish p {
    font-weight: 600;
    margin-block-end: 2rem;
  }
  .finish p span {
    padding: .3rem;
    box-shadow: var(--shadow-1);
    background: var(--green-color);
    color: var(--white-color);
    margin-left: .5rem;
  }
  .finish button {
    text-transform: uppercase;
    transition: var(--transition);
  }
  .finish button:hover {
    background: var(--green-color);
  }
  

</style>
