<template>
	<div class = 'main'>
		<div class="questions" :class = "{'showResult':!showResult}">
			<h2>{{Ql[index].title}}</h2>
			<img :src = "Ql[index].img" :class = "{'hidden':!hidden}">
			<button class = "btn-select fact" @click = "userAnswer.push(true);showAnswer();" :class = "{'hidden':!hidden}">Факт</button>
			<button class = "btn-select fake" @click = "userAnswer.push(false);showAnswer();" :class = "{'hidden':!hidden}">Фейк</button>
			<p  :class = "{'hidden':hidden, 'err':err, 'right':right}"><span class = "feedback"><p>{{Ql[index].feedback}}</p></span>
			<a :href="Ql[index].proof" :class = "{'hidden':hidden}" target="_blank">Посилання</a>
			</p>
			
			<button @click = "showNext(); hidden = !hidden" class = "btn" :class = "{'hidden':hidden}">Далі</button>
		</div>
		<div :class="{'showResult':showResult}" class = "result">
			<h2>Ваш результат: {{count}}/{{index+1}}</h2>
			<p>{{comment}}</p>
			<a class = "btn" href="/">Спробувати ще раз</a>
		</div>
	</div>
	
</template>

<script>
	export default{
	data(){
		return{
			Ql:[ //questions list
				{	
					title: 'ЗНО відмінили через карантин',
					feedback:'Це фейк. 1 квітня був поширений підроблений документ МОН, в якому відомство нібито передбачало проведення «перевірки знань учасників освітнього процесу, засвоєних у ході дистанційного навчання за технологією ЗНО для всіх учнів 5-11 класів». МОН заперечило цю інформацію та наголосило, що ЗНО відбудеться незалежно від термінів діючого карантину через COVID-19. Деталі можна дізнатися на сайті МОН.',
					proof:'https://mon.gov.ua/ua/news/stop-fejk-mon-nagoloshuye-sho-karantin-trivaye-do-24-kvitnya-zno-vidbudetsya-nemaye-rekomendovanih-platform-dlya-distancijnogo-navchannya-zhodnih-specperevirok-znan-zdobutih-pid-chas-karantinu',
					img: require('@/assets/img/q1.jpg'),
					correct: false,
					
				},
				{	
					title: 'На Поділлі існує затоплене село. ', 
					feedback:'Бакота — затоплене село на Поділлі, поблизу Кам’янця-Подільського. Сьогодні це місце відоме своїми неймовірними краєвидами та тишею. Півсторіччя тому сотні родин покинули тут свої домівки та господарства. Людей виселили, а село затопили, щоби збудувати тут водосховище для потужної гідроелектростанції. Більше про Бакоту можна дізнатися за посиланням.',
					proof:'https://ukrainer.net/bakota/',
					img: require('@/assets/img/q2.png'),
					correct: true,

				},
				{	
					title: 'Президент України Володимир Зеленський вигнав із зали секретаря Бориспільської міськради зі словами «Йди гуляти, розбійнику. Погано чуєш мене?» ', 
					feedback:'Під час наради з питань розвитку Київської області та міста Борисполя відбулась словесна сутичка між президентом Зеленським та секретаром міськради Борисполя Ярославом Годунок, у фіналі якої перший вигнав другого із зали. Детально про ситуацію можна прочитати за посиланням.',
					proof:'https://www.pravda.com.ua/articles/2019/08/14/7223494/',
					img: require('@/assets/img/q3.jpg'),
					correct: true
				},
				{	
					title: 'Вчені довели користь гомеопатії. Було проведено безліч детальних досліджень щодо гомеопатії як наукового прориву року', 
					feedback:'Фейк. Про це повідомляє МОЗ України . На сьогоднішній день немає надійних доказів ефективності гомеопатії при будь-яких захворюваннях. Дієвість гомеопатичного теоретично необґрунтованого способу лікування сьогодні не доведена. Поки не буде доведено науковість гомеопатії, вона залишається поза медицини.',
					proof:'https://moz.gov.ua/article/health/5-najpopuljarnishih-medichnih-mifiv',
						img: require('@/assets/img/q4.jpg'),
					correct: false
				},
				{	
					title: 'Українці у 2019 році стали другими у світі за зростанням кількості замовлень на AliExpress',
					feedback:'Кількість замовлень українців із AliExpress за 10 місяців 2019 року зросла на 70%. Це вивело Україну на 2 місце за темпами зростання на маркетплейсі. За загальною вартістю проданих товарів на AliExpress у 2019 році Україна ввійшла у ТОП-10 країн світу. Про регіони, у які доставили найбільше посилок, можна дізнатися на сайті Укрпошти .',
					proof:'https://ukrposhta.ua/alibaba-bye-rekordi-v-ukra%D1%97ni-ukra%D1%97nci-stali-2-u-sviti-za-zrostannyam-kilkosti-zamovlen-na-aliexpress/',
					img: require('@/assets/img/q5.jpg'),
					correct: true
				},
				{	
					title: 'Екс-президент України Петро Порошенко став співвласником популярного гумористичного концертного шоу «Дизель-шоу»',
					feedback:'Цю «новину» взяли із сайту сатиричних новин UaReview, що відкрито позиціонує себе як ресурс смішних вигаданих матеріалів, які не можна сприймати як правдиві. Редакція сайту наголошує, що всі згадані на сайті події та персонажі вигадані, а будь-який збіг з реальними подіями та людьми є випадковим. Багато українських ЗМІ не перевірили інформацію, натомість підхопили та швидко поширили. Сам UaReview закликає усіх більше дізнаватися про фейкові новини та розвивати своє критичне мислення. ',
					proof:'https://ms.detector.media/manipulyatsii/post/23678/2019-10-22-nizka-zmi-poshirili-feik-pro-kupivlyu-poroshenkom-proektu-dizel-shou/',
					img: require('@/assets/img/q6.png'),
					correct: false
				},
				{	
					title: 'У Києві біля моста Патона з’явилися дельфіни',
					feedback:'Це фейк, оскільки оригінал цього короткого відео належить користувачеві під ніком Matt Wiles, який, судячи з даних його особистої сторінки, живе у Великобританії і займається риболовлею. Два схожих відео з дельфінами він опублікував 11 квітня 2020 року і прокоментував їх так: «Dolphins on the way back in» («Дельфіни на шляху назад»). Більше про аналіз звуків хвиль та чайок за посиланням .',
					proof:'https://www.stopfake.org/uk/fejk-u-kiyevi-bilya-mosta-patona-z-yavilisya-delfini/',
					img: require('@/assets/img/q7.png'),
					correct: false
				},
				{	
					title: 'Різдвяна пісня Carol of the Bells має походження від української народної пісні «Щедрик». Факт чи фейк?',
					feedback:'У 1921-му «Щедрик» Петра Вільховського вперше почули у США – в нью-йоркському Карнегі Холі. А у 1936 році народна щедрівка, музику до якої написав Микола Леонтович, стала всесвітньо відомою під назвою «Carol of the Bells». У «Щедрика» є п’ять авторських варіантів, а сам композитор присвятив їй 18 років життя: перший варіант з’явився 1901 року, а останній – 1919-го.',
					proof:'https://uk.wikipedia.org/wiki/%D0%A9%D0%B5%D0%B4%D1%80%D0%B8%D0%BA_(%D0%9B%D0%B5%D0%BE%D0%BD%D1%82%D0%BE%D0%B2%D0%B8%D1%87',
					img: require('@/assets/img/q8.jpg'),
					correct: true
				},
				{	
					title: 'Україна повністю готова до коронавірусу',
					feedback:'Фейк. На даний момент немає жодної країни у світі, яка була б повністю готова до відповіді на коронавірус. Приклад США, Італії, Іспанії чи Німеччини свідчить про те, що кожна країна стикається зі схожими проблемами. Але, якщо говорити про підготовку до пандемії, зокрема роботу уряду, особливо що стосується забезпечення тестами та оснащення лікарень, то на жаль, українська влада поки що програє корона вірусу.',
					img: require('@/assets/img/q9.png'),
					proof:'https://ukrainer.net/covid-19/',
					correct: false
				},
				{	
					title: 'В Україні зіграли перше онлайн-весілля.',
					feedback:'Факт. У Львові відбулося перше в Україні онлайн-весілля – одружилися наречені Інна та Ігор. На церемонії укладання шлюбу були лише ведучий, фотограф і діджей. Батьки наречених були по той бік екрану – від них, за традицією, пролунав перший тост і благословення. Весільний стіл лише для двох, проте 70 гостей з п’яти країн світу долучилися до свята Інни та Ігоря через інтернет. Налагодити відеозв’язок вдалося навіть 90-річній бабусі нареченої.',
					proof:'https://shotam.info/v-ukraini-zihraly-pershe-onlayn-vesillia/',
					img: require('@/assets/img/q10.jpg'),
					correct: true
				},
				{	
					title: "У березні 2018 року в інтернеті набуло популярності чорно-біле фото, на якому зображені три дівчини. У підписі говорилося, що це канцлер Німеччини Ангела Меркель, прем'єр-міністр Великобританії Тереза Мей і президент Литви Даля Грібаускайте.",
					feedback:"Фейк. Канцлер Німеччини Ангела Меркель народилась у 1954 році, президент Литви Даля Ґрібаускайте – у 1956-му. Так, у 1992 році їм мало виповнитись, відповідно, 38 і 36 років. Однак, як ми вже дізнались раніше, на представленій світлині Ангелі Меркель лише 18 років, а зроблена вона була в 1972 році.",
					proof:'https://www.radiosvoboda.org/a/29128740.html ',
					img: require('@/assets/img/q10.jpg'),
					correct: true
				},
						
			],
			userAnswer:[],
			index:0,
			hidden: true,
			right: false,
			err: false,
			count: 0,
			showResult: true,
			comment:''
		}
	},

	methods:{

		showAnswer(){
			
			let index = this.index;
			this.hidden = !this.hidden;
			if(this.userAnswer[index] == this.Ql[index].correct){
				this.err = false;
				this.right = true;
				this.count+=1;
				
			}else{
				this.right = false;
				this.err = true
			}
			
			
		},

		showNext(){

			if (this.index == this.Ql.length-1){
				this.hidden = true; 
				this.showResult = !this.showResult
				console.log(this.count);
				if (this.count == 0){
					this.comment = "Результат не втішний, але є добра новина: скільки нового Ви дізналися! Що гомеопатія – це не наука, що українці дуже полюбляють замовляти з Китаю, а українська народна пісня відома на весь світ. Починайте вчитися аналізувати інформацію, яку споживаєте. Опанувати редакторові, що таке факт, фейк, критичне мислення можна на дисциплінах «Медіакультура», «Інформаційні війни», «Типологія помилок», «Літературне редагування», «Теорії масової інформації».";
				} else if (this.count <= 2){
					this.comment = "Краще, ніж нічого! Проте є куди зростати. Вдосконалюйте критичне мислення, вчіться об’єктивно аналізувати інформацію. Перевіряйте публікації, якщо сумніваєтесь у їх достовірності, і будете щасливі та не обдурені 😉 Дізнатися більше як відрізнити фейк від факту можна на дисциплінах «Медіакультура», «Інформаційні війни», «Типологія помилок», «Літературне редагування», «Теорії масової інформації».";
				}else if (this.count <= 5){
					this.comment = "Непоганий результат! Інформацію з новинної стрічки Ви не сприймаєте за чисту монету. Не забувайте перевіряти дані у першоджерелі: це стосується цитат з книг, суджень про наукові відкриття, посилань на офіційні документи. Як боротися з розповсюдженням фейків можна дізнатися на дисциплінах «Медіакультура», «Інформаційні війни», «Типологія помилок», «Літературне редагування», «Теорії масової інформації».";
				}else if (this.count <= 8){
					this.comment = "Це навіть більше ніж добре! Ви ставитесь скептично до матеріалів ЗМІ, не піддаєтеся провокації та перевіряєте факти, на яких засновані новинні сюжети. Як фейки керують емоціями та чому варто уважно ставитися до матеріалів, що викликають сумніви, розглядається на парах дисциплін «Медіакультура», «Інформаційні війни», «Типологія помилок», «Літературне редагування», «Теорії масової інформації».";
				} else {
					this.comment = "Ой леле, та Ви ж майстер фактчекінгу! Вас складно надурити, Ви піддаєте будь-яку інформацію критиці. Перед тим як поширити новину серед інших, Ви декілька разів все перевірите. Так тримати! Ще більше прикладів фейків у ЗМІ розглядається на парах дисциплін «Медіакультура», «Інформаційні війни», «Типологія помилок», «Літературне редагування», «Теорії масової інформації».";
				}


			}
			else{
				this.index++;	
				
			}
		}
	}
}
</script>

<style>
h2{
	
	color:#2d3f53;
	font-weight: 300;
	margin: 0.5rem;

	font-size: 25px;
}
p{	
	color:#2d3f53;
	font-weight: 400;
	font-size: 16px;
	display: block;
	

}

.feedback p{
	text-align: justify;
	text-indent: 20px;
	word-spacing: 3px;
	padding: 0;
}

img{
	
	max-width: 420px;
	max-height: 320px;
	display: block;
	margin: 0 auto;
}
a{
	display: block;
	text-align: center;
	text-indent: 0;
	padding: 0;
}
.home{
  width: 550px;
  max-width: 800px;
  min-width: 250px;
  background-color: #fff;
  padding: 1rem;
  margin: 0 auto;
  text-align: center;
  margin-top: 2rem;
  margin-bottom: 2rem;
  border-radius:0.3rem;

}
.main{
	background-color: #fff;
}
/*DYNAMIC CLASS*/
.hidden{
	display: none;
}
.showResult{
	display: none;
}
/*BUTTONS*/
.btn-select{
	font-family: Roboto Slab,serif;
	font-size: 16px;
	font-weight: 500;
	letter-spacing: .075em;
	line-height: 2.5em;
	text-align: center;
  	text-decoration: none;
  	text-transform: uppercase;
	margin: 0 auto;
	margin: 0.5rem;
	cursor: pointer;
	vertical-align: middle;
  	border:none;
  	outline: none;
  	background-color: transparent;
  	border-radius: 0.3rem;
}
.fact{
	border:0.2rem solid #61d145;
	color: #83f567;
}
.fake{
	border:0.2rem solid #ff5454;
	color: #ff8563;
}
.fake:hover{
	background-color: #ff5454;
	color:#fff;
}

.fact:hover{
	background-color: #61d145;
	color:#fff;
}

.btn-select:active{
	top:5px;
}


/*ANSWER WINDOW*/
/*IF MISTAKE*/
.err{
	display: block;
}

.err::before{
	content:'╳  Не правильно ';
	display: block;
	font-weight: 900;
	color:#ff8563;
	margin: 0px 25px 10px 25px;
	border-bottom:3px solid #ff8563;
	text-align: center;
	text-indent:0;
}

.err::after{
	content: '';
	display: block;
	color:#ff8563;
	margin: 10px 25px 0px 25px;
	border-bottom:3px solid #ff8563;
}
/*IF RIGHT*/
.right{
	display: block;
}
.right::before{
	content:'✓ Правильно ';
	display: block;
	font-weight: 600;
	color:#83f567;
	margin: 0px 25px 10px 25px;
	border-bottom:3px solid #83f567;	
	text-align: center;
	text-indent: 0;

}


.right::after{
	content:' ';
	display: block;
	font-weight: 600;
	color:#ff8563;
	margin: 10px 25px 0px 25px;
	border-bottom:3px solid #83f567;
	text-indent:0;
}

.result h2{
	font-weight: 600;
}
.result p{
	text-align: justify;
	text-indent: 1.5em;
}

@media screen and (max-width: 500px){
  body{overflow-y: scroll;}
 
  img{
    width: 280px;
    height: 200px;
    
  }

  h2{
    font-size: 18px;
  }

  p{
    font-size: 14px;
    padding:0px 10px 0px 10px;
  }

  .btn{
    font-size: 14px;
  }
  .home{
    width: 300px;
    padding: 0.1rem;
  }
  .btn-select{
    font-size:14px; 
  }
}
</style>