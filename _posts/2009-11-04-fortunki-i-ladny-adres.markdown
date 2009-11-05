---
layout: post
title: Fortunki i przyjazny adres
---

#{{ page.title }}

Postaram się szybko streścić w jaki sposób uzyskałem możliwość dostępu do fortunek z kategorii np. "Jokes" poprzez np. taki adres localhost:3000/Jokes.
<br />
W założeniach mamy 2 modele: Quotation oraz Category. Relacja miedzy nimi bedzie jeden-do-wielu.<br />
Do modelu Category dodajemy w tym celu:
{% highlight ruby %}
  has_many :quotations
{% endhighlight %}
A do modelu Quotation:
{% highlight ruby %}
  belongs_to :category
{% endhighlight %}
Oczywiście tabela Quotations musi mieć kolumnę category_id.
<br />
Przechodząc do sedna sprawy, dodajemy w routes.rb wpis: 
{% highlight ruby %}
  map.connect ':category', :controller => 'quotations', :action => 'index'
{% endhighlight %}
A w quotations_controller.rb:
{% highlight ruby %}
  unless params[:category].nil?
    @quotations = Category.find_by_name(params[:category]).quotations
  else
    @quotations = Quotation.all
  end
{% endhighlight %}
Dzięki temu, jeśli przejdziemy pod konkretny adres kategorii, jako parametr dosteniemy nazwe. To umożliwi nam pobranie wszystkich fortunek danej kategorii, w przypadku normalnego wywołania quotations GET, params[:category] jest pusty, więc pobieramy wszystkie fortunki.
