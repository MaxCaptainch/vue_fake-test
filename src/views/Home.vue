<template>
  <div class="home">
  	<div :class = "{'hidden':!hidden}">
    <div class="helloWindow">
    <h2>Факт чи фейк?</h2>
    <p>Сучасні ЗМІ переповнені фейками та фактами, що іноді сумніваєшся у правдивості отриманої інформацію. Чи дійсно ЗНО скасували через карантин? Чи правда, що існує затоплене село на Поділлі? </p>
    <p>Редактору видання важливо не допустити потрапляння фальсифікації на шпальту. Тому потрібно вміти мислити критично та бути уважним до деталей. </p>
    <p>Пройдіть тест та спробуйте дізнатися, чи зможете відрізнити правду від вигадки.</p>
    </div>
    <button class="btn" v-on:click="hidden = !hidden;">Почати</button>
    </div>
    <Questions :class = "{'hidden':hidden}" />
  </div>
</template>

<script>
// @ is an alias to /src
import Questions from '@/components/Questions.vue'

export default {
	data(){
  	 	return{
  	 	hidden: true
  	 	}
  	},	

  	name: 'Home',
  	components: {
     	Questions
 	},
  
  	
}


</script>

<style>
.btn {
 
  display: block;
  font-family: Roboto Slab,serif;
  font-weight: bold;
  font-size: 14px;
  font-weight: 700;
  letter-spacing: .075em;
  line-height: 2.5em;
  text-decoration: none;
  text-transform: uppercase;
  white-space: nowrap;
  color: #2d3f53;
  cursor: pointer;
  vertical-align: middle;
  margin:0 auto; 
  margin-top: 0.2rem;
  margin-bottom: 0.5rem;
  border-radius: .375em;
  outline: none;
  border:2px solid #2d3f53;
  background-color: transparent;
}


.btn:active{
	top:5px;
}

.hidden{
	display: none;
	
}
.helloWindow h2{
  font-weight: 600;
}

.helloWindow  p{
  text-align: justify;
  text-indent: 1.5em;
}



</style>