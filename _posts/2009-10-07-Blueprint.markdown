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
Ideą Blueprinta jest podzielenie strony na siatkę, która z kolei może mieć do 24 kolumn, gdzie każda z nich ma szerokość 30px.
Oddzielone są od siebie 10px marginesem. Do obsługi tego korzystamy z klasy 'span-...', gdzie w miejsce wielokropka wstawiany na jak 
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

####Przykładowa strona
<a href="http://sigma.ug.edu.pl/~bdrzazgo/blueprint/">Tutaj</a> można znaleźć moją przykładową stronę wykorzystującą Blueprinta. 

####Podsumowanie
Myślę, że Blueprint jest tego typu frameworkiem, który zapewnia, że czas poświecony na jego naukę może bardzo szybko się zwrócić. 
Dodatkowym atutem jest kopatybilność z wszystkimi najpopularniejszymi obecnie przeglądarkami(<a href="http://wiki.github.com/joshuaclayton/blueprint-css/browser-compatibility-list">żródło</a>).

### Unused selectors
Po uruchomieniu wtyczki wyszukującego nieużywane elemnty CSS'a oczom mym ukazał się taki oto widok:

<img src="../../../../images/ucss.png" alt="unusedcss" />


###Walidacja strony
Przeprowadziłem walidacje strony pod kątem kodu html. Test pomyślnie zakończony ;)<br />
CSS także został zwalidowany, nie obylo sie bez paru warningow, ale test został zakończony pomyślnie.

<p style="float: left; margin-right: 10px">
 <a href="http://validator.w3.org/check?uri=referer"><img
        src="http://www.w3.org/Icons/valid-xhtml10-blue"
        alt="Valid XHTML 1.0 Strict" height="31" width="88" /></a>
</p>
<p>
<a href="http://jigsaw.w3.org/css-validator/check/referer">
    <img style="border:0;width:88px;height:31px"
        src="http://jigsaw.w3.org/css-validator/images/vcss-blue"
        alt="Valid CSS!" />
</a>
</p>

###YSlow  
W tescie YSlow blog otrzymał note: C. W wiekszości kategorii było dobrze, czyli A. Niespodobało mu się m.in. to, że css nie są spakowane gzipem i nie ma Expires headers. Z tego co wyczytałem to te opcje ustawia sie w apache'u, więc ogólnie nie jest źle ;)

### Linki
  <a href="http://www.blueprintcss.org/">Strona domowa projektu</a><br />
  <a href="http://github.com/joshuaclayton/blueprint-css">Blueprint na Github'ie</a>
