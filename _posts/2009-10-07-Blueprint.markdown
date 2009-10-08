---
layout: post
title: Blueprint
---

# {{ page.title }}

## Blueprint

Blueprint jest to framework CSS, który pozwoli nam na znacznie oszczędzenie czasu podczas tworzenia layout'u strony, tym samym
dając możliwość skupienia sie na treści merytorycznej strony. Plusem może być także obsługa pluginów, które można znaleźć chociażby 
na Github'ie.

####Kolumny
Ideą Blueprinta jest podzielenie strony na kolumny, możemy mieć do 24 takich kolumn, gdzie każda z nich ma szerokość 30px.
Oddzielone są od siebie 10px marginesem. Aby obsługi tego korzystamy z klasy 'span-...', gdzie w miejsce wielokropka wstawiany na jak 
wiele kolumn bedzie szeroki nasz div. Span-1 oznacza kolumne szerokości 30px, zaś span-2 to już 70px(2 kolumny + margines 10px).<br />
Powiedzmy, że chcemy stworzyć szablon z 2 kolumnami o szerokości 150px oraz 710px, przykładowy kod może wyglądać następująco:
{% highlight html  %}
  <div class="container">
    <div class="span-4">
	  Lewa kolumna o szerokości 150px.
	</div>
	<div class="span-18">
	  Prawa kolumna o szerokości 710px.
	</div>
  </div>
{% endhighlight %}

W łatwy sposób stworzymy podstawowy szablon strony z nagłowkiem, stopką, menu oraz zawartością:
{% highlight html %}
  <div class="container">
    <div class="span-24 last">
	  Nagłówek
    </div>
    <div class="span-5">
	  Menu
    </div>
    <div class="span-19 last">
	  Zawartość
    </div>
    <div class="span-24 last">
  	  Stopka
    </div>	
  </div>
{% endhighlight %}
Klasa 'last' usunie prawe marginesy, dzięki czemu lepiej dopasujemy nasze elementy do całości.
Plik CSS zawierający powyższe klasy można znaleźć <a href="http://github.com/joshuaclayton/blueprint-css/blob/master/blueprint/src/grid.css">tutaj</a>.

####Formularze
Blueprint umożliwia także przyjemniejszą prace z formularzami. Udostępnia klasy opakowujące div'y z komunikatami takimi jak: error, notice czy success, 
które są bardzo przyjemne dla oka.
Funkcjonalności te znajdziemy w pliku <a href="http://github.com/joshuaclayton/blueprint-css/blob/master/blueprint/src/forms.css">form.css</a>

####Styl tekstu
Standardowo w Blueprint wysokość linii określona jest jest na 18px, co oznacza, że wysokość każdego elementu musi być podzielna przez 18.
Jak wygląda to w akcji można zobaczyć <a href="http://www.blueprintcss.org/tests/parts/elements.html">tutaj</a>

####Podsumowanie
Myślę, że Blueprint jest tego typu frameworkiem, który zapewnia, że czas poświecony na jego naukę może bardzo szybko się zwrócić. 
Dodatkowym atutem jest kopatybilność z wszystkimi najpopularniejszymi obecnie przeglądarkami(<a href="http://wiki.github.com/joshuaclayton/blueprint-css/browser-compatibility-list">żródło</a>).

## Linki
  <a href="http://www.blueprintcss.org/">Strona domowa projektu</a><br />
  <a href="http://http://github.com/joshuaclayton/blueprint-css">Blueprint na Github'ie</a>
