---
layout: post
title: Projekt Euler
---

# {{ page.title }}

Jako, że na fakultecie korzystać będziemy z języka Ruby, przydałoby sie go w miare sensownie opanować. Kiedy znamy już jakieś podstawy, 
polecam w tym celu polepszenia swoich umijętności pobawienie się z zadaniami na stronie <a href="http://projecteuler.net">Projektu Euler</a>.
Strona ta zawiera róznego rodzaju problemy matematyczne czy infomatyczne, które możemy rozwiązać za pomocą każdego języka programowania. 
A to dlatego, że jako rozwiązanie podajemy tylko wynik, nie zaś cały kod.
Przedstawie tutaj pierwsze zadanie: 
<pre>
  If we list all the natural numbers below 10 that are multiples of 3 or 5, 
  we get 3, 5, 6 and 9. The sum of these multiples is 23.
  Find the sum of all the multiples of 3 or 5 below 1000.
</pre>
Tak więc musimy znaleźć sumę liczby które dzielą się przez 3 lub 5 i są mniejsze od 1000. W Ruby'm nie bedziemy mieli z tym wiekszego problemu:
{% highlight ruby %}
  p (1...1000).select() { |n| n % 3 == 0 || n % 5 == 0 }.inject(:+)
{% endhighlight %}
Jak widzimy 1 linijka i zadanie rozwiązane :)

Jeśli ktoś byłby zainteresowany to rozwiązania parunastu problemów są umieszczone na moim <a href="http://github.com/Drzazga/Euler">Github'ie</a>
