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
    },
    {
      question: 'Qual a raiz quadrada de 5?',
      answer: 4,
      options: [
        '5',
        '25',
        '2.24'
      ],
      selected: null
    },
    {
      question: 'Qual é a base de 5 elevado a 2?',
      answer: 3,
      options: [
        '25',
        '15',
        '125'
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

</script>
  
<template>

  <h1>vue</h1>

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
        appearance: none;
        font-family: 'Poppins', sans-serif;
    }

  /*==========Base==========*/
  :root {

    --primary-color: hsl(25, 76%, 90%);
    --dark-color: hsl(0, 0%, 13%);
    --black-color: hsl(0, 0%, 0%);
    --white-color: hsl(0, 0%, 100%);
    --green-color: hsl(154, 100%, 81%);
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
    height: 300rem;
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

</style>
