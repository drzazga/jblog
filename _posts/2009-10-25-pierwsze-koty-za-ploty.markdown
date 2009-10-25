---
layout: post
title: pierwsze-koty-za-ploty 
---

# {{ page.title }}
Po chwilowej zabawie z haml'em i sass'em postanowiłem się wziąć za coś ciekawszego, zacząłem tworzyć aplikację z kolejnego ćwiczenia.

####Startujemy

Zaczynamy standardowo:
{% highlight bash %}
rails kontakty
cd rails
./script/generate scaffold contact first_name:string surname:string email:string gg:integer homepage:string phone:string city:string street:string post_code:string
rake db:migrate
./script/server
{% endhighlight %}

Po odpaleniu strony z kontaktami, przetestowałem ją YSlow, wynik 96pkt(nota A).

####install_theme
Teraz przyszła pora na jakiś ładniejszy layout, wybór padł na <a href="http://www.oswd.org/design/preview/id/3551">ten</a><br />
Po jego drobnych modyfikacjach, użyłem narzędzia install_theme, aby dodać theme do mojej aplikacji:
{% highlight bash %}
install_theme . ../../LoadFoO/ "#left:text" --partial menu:#menu --partial last:#lastUpdated
{% endhighlight %}
Postaram się teraz nieco wyjaśnić powyższy kod.<br />
<ul>
<li>"#left:text" to nasz div robiący jako content, dodany zostanie tam railsowy yield, a kod generowany przez inne widoki będzie trafiał własnie tam. </li>
<li> --partial menu:#menu tworzy partial odpowiedzialny za menu </li>
<li> --partial last:#lastUpdate stworzy partial, dzieki któremu wyświetlać będę ostanio zmienianie kontakty </li>
</ul>

####Gravatary
Zaczynamy od zainstalowania pluginu:
{% highlight bash %}
./script/plugin install git://github.com/mdeering/gravatar_image_tag.git
{% endhighlight %}
Następnie dodałem wpisy do pliku config/initializes/gravatar_defaults.rb
{% highlight ruby %}
ActionView::Base.default_gravatar_image  = "http://gen2.org/~dogrizz/default_gravatar.png"
ActionView::Base.default_gravatar_size = 50
{% endhighlight %}
Pierwszy wpis to ścieżka do defaultowego obrazka, w razie gdy user nie miałby swojego gravatara. Drugi wpis ustawia wielkość gravatara.
<br />Aby umieścić gravatar na stronie wystarczy wpisać:
{% highlight erb %}
  <%= gravatar_image_tag("jakis@email.com") %> 
{% endhighlight %}
Możemy też określić wielkość gravatara w ten sposob:
{% highlight erb %}
  <%= gravatar_image_tag("jakis@email.com", :gravatar => { :size => 30 }) %> 
{% endhighlight %}

####Geolocation
Aby dodać geolokalizacje potrzebny będzie nowy model Address, tak więc usunąłem pola city, street i post_code z modelu contact:
{% highlight bash %}
./script/generate migration RemoveCityStreetPostCodeFromContact city:string street:string post_code:string
{% endhighlight %}
Tworzy nowy model wedle tego co jest na stronie pluginu:
{% highlight bash %}
./script/generate model Address street:string locality:string city:string state:string country:string zip:string lat:string lng:string
{% endhighlight %}
Potem dodajemy odpowiedni formularz i ... <br />
Lipa, u mnie nie trybi, tak więc ogólnie szału nie ma ;)

