---
layout: post
title: pierwsze-koty-za-ploty 
---

# {{ page.title }}
Po chwilowej zabawie z haml'em i sass'em postanowiłem się wziąć za coś ciekawszego, zacząłem tworzyć aplikację z kolejnego ćwiczenia.<br />
Kod aplikacji znajduje się na <a href="http://github.com/Drzazga/kontakty">Github'ie</a>

####Startujemy

Dzięki uprzejmości Szymona postawiłem ten prjekt pod adresem: <a href="http://gen2.org:9876/">http://gen2.org:9876/</a>.<br />

Zaczynamy standardowo:
{% highlight bash %}
rails kontakty
cd kontakty
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
Lipa, u mnie nie trybi, tak więc ogólnie szału nie ma ;)<br /><br />
Po krótkich poszukiwaniach znalazłem inny gem: Geokit.
Instalujemy jako plugin lub gem:
{% highlight bash %}
./script/plugin install git://github.com/andre/geokit-rails.git
{% endhighlight %}
lub dodajemy 
{% highlight ruby %}
Rails::Initializer.run do |config|
...
config.gem "geokit"
...
end
{% endhighlight %}
do pliku environment.rb, a potem:
{% highlight bash %}
rake gems:install
{% endhighlight %}
Następnie w pliku config/initializers/geokit_config.rb musimy dodać nasz wygenerowany klucz dla Google Maps, pobrać go można z http://www.google.com/apis/maps/signup.html.
Pozostaje nam dodać gdzieś kod odpowiedzialny za geolokalizacje, więc w jakimś kontrolerze(w zależności gdzie chcecie pózniej wyświetlić dane) piszemy:
{% highlight ruby %}
@location = Geokit::Geocoders::MultiGeocoder.geocode(request.remote_ip)
{% endhighlight %}
Dzięki temu w widokach będziemy mogli korzystać z tej zmiennej, np:
{% highlight erb %}
You are probably from: <%= @location.city %><br />
 Country: <%= @location.country_code %>
{% endhighlight %}
U mnie pokazało, że jestem z Wawy, ale ważne, że działa ;)

####Paginacja
Super mega geolokacja mi nie działa, więc postanowiłem dodać coś innego do aplikacji a mianowicie paginacje do kontaktów na stronie głównej.<br />
Posłużymy się gemem mislav-will_paginate. Aby go zainstalować wrzucamy do pliku config/environment.rb wpis:
{% highlight ruby %}
  Rails::Initializer.run do |config|
    ...
    config.gem 'will_paginate', :version => '~> 2.3.11', :source => 'http://gemcutter.org'
    ...
  end
{% endhighlight %}
Pózniej rake gems:install i możemy się cieszyć z zainstalowanego gemu :)
Do kontrolera gdzie pobierałem kontakty dodałem wpis:
{% highlight ruby %}
  @contacts = Contact.paginate :per_page => 5, :page => params[:page], :order => 'updated_at DESC'
{% endhighlight %}
Powyższy wpis mówi, że będziemy wyświetlać na strone po 5 kontaków posortowanych według daty modyfikacji.<br />
Pozostaje nam jedynie dodać do pliku index.html.erb wpisu:
{% highlight erb %}
  <%= will_paginate @contacts %>
{% endhighlight %}
Jeśli zamiast "Next" i "Previous" chcemy mieć polskie nazwy to wpisujemy:
{% highlight erb %}
  <%= will_paginate @questions, { 
    :previous_label => 'Poprzednie', 
   :next_label => 'Następne' 
  } %>
{% endhighlight %}
I to by było na tyle jeśli chodzi o paginacje :)

####Authlogic + Lockdown
Dodałem obłsugę autentykacji(Authlogic) oraz autoryzacji(Lockdown).
Póki co nie mam czasu pisać co i jak zrobić, więc zarzucę jedynie linkami: <br />
<a href="http://github.com/binarylogic/authlogic_example">Authlogic</a><br />
<a href="http://stonean.com/">Lockdown</a>

####Asset Packager
Po spakowaniu plików js oraz css pluginem, w tescie YSlow otrzymałem notę B(86 pkt). "Make fewer HTTP requests" otrzymało notę A, tak więc plugin spełnił swoje zadanie :)   

####Tagi
Skorzystałem z pluginu acts_as_taggable_on_steroids, aby obsługiwać tagi.
