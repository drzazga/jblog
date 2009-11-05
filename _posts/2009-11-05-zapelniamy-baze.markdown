---
layout: post
title: Zapełniamy bazę kontaktami
---

#{{ page.title }}

Kiedy mamy już skończoną naszą aplikację przydałoby się zapełnić bazę jakimiś kontaktami. Przedstawie sposób na łatwe i szybkie dodawanie wielu kontaktów do naszej bazy. Railsy 2.3.4 natywnie zaczęły wspierać tą czynność, dodając plik db/seeds.rb.<br />
Potrzebować będziemy jeszcze gemu Facker, który dostarczy nam imiona, nazwiska etc. Instalujemy go więc:
{% highlight bash %}
 sudo gem install faker
{% endhighlight %}
API do Facker'a znajdziecie <a href="http://faker.rubyforge.org/rdoc/">tutaj</a>
Pozostaje nam teraz dokonać odpowiednich wpisów w seeds.rb, mój przykładowy plik wygląda tak:
{% highlight bash %}
require 'faker'

Contact.delete_all

1.upto(100) do 
  Contact.create(
    :user_id => User.first.id,
    :first_name => Faker::Name.first_name,
    :surname => Faker::Name.last_name,
    :phone => Faker::PhoneNumber.phone_number,
    :email => Faker::Internet.email,
    :homepage => Faker::Internet.domain_name,
    :city => Faker::Address.city,
    :street => Faker::Address.street_name,
    :post_code => Faker::Address.zip_code,
    :category_id => Category.first.id
  ) 
end 
{% endhighlight %}
Na koniec wpisujemy w konsoli:
{% highlight bash %}
 rake db:seed
{% endhighlight %}

