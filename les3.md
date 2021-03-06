---
layout: default
title: Les 3
---

#Les 3: Cipher

Al duizenden jaren proberen mensen elkaar berichten te versturen die niet door anderen mogen worden gelezen.

Een van de oudste manieren zou door Julius Caesar zelf zijn gebruikt en is redelijk eenvoudig. Hij schoof elke letter in een bericht een vast aantal plaatsen door in het alfabet. Dus hij maakte bijvoorbeeld van een 'a' een 'd', van een 'b' een 'e' etc. Met deze methode gaan we in deze opdracht aan de slag. Zie ook: [Caesar Cipher op wikipedia](http://en.wikipedia.org/wiki/Caesar_cipher).

In deze les behandelen we:

* This will become a table of contents (this text will be scraped).
{:toc}

##Bestanden

In deze map vind je de volgende bestanden:

    readme.html - deze beschrijving
    cipher.rb - het script waar je in gaat werken
    encrypted_message.txt - het versleutelde bestand met shift 12
    encrypted_brute_force.txt - voor de laatste opdracht

## Informatie

### Arrays
Een `Array` is een geordende collectie.

{% highlight ruby %}
namen = ["Harrie", "Maria", "Evelien", "Piet"]
{% endhighlight %}

Je spreekt een voorwerp uit een array aan met de index. Het eerste voorwerp uit de array correspondeert met index 0. 

{% highlight ruby %}
namen[0]    # => "Harrie"
namen[2]    # => "Evelien"
{% endhighlight %}

-1 correspondeert met het laatste element uit de array.

{% highlight ruby %}
namen[-1]   # => "Piet"
{% endhighlight %}

N.B. Je kunt ook strings op deze manier aanspreken!

{% highlight ruby %}
naam = "Jan"
naam[0]     # => "J"
{% endhighlight %}

### For Loops
Als je een opdracht een vast aantal keer uit moet voeren, gebruik je een for loop. Stel dat je elk element uit een array wilt aanspreken:

{% highlight ruby %}
for naam in namen do
    puts "Hallo, #{naam}!"
end
# => "Hallo, Harrie!"
# => "Hallo, Maria!"
# => "Hallo, Evelien!"
# => "Hallo, Piet!"
{% endhighlight %}

Je kunt ook over een _range_ itereren. Experimenteer met de volgende loops in `irb`.

{% highlight ruby %}
for number in (0..100) do
    puts number
end

for letter in ("a"..."z")
    puts letter
end
{% endhighlight %}

Wat is het verschil tussen `(0..10)` en `(0...10)`?

### Hashes
Een `Hash` lijkt op een array, maar je spreekt een waarde uit de collectie niet aan met een index, maar met een _key_. Een key kan van elk datatype zijn. De volgende hash verbindt landen met hun hoofdsteden:

{% highlight ruby %}
hoofdsteden = {
    "Nederland" => "Amsterdam",
    "Frankrijk" => "Parijs",
    "Slowakije" => "Bratislava"
    }

hoofdsteden["Nederland"]    # => "Amsterdam"   
{% endhighlight %}

`"Nederland"` en `"Amsterdam"` worden samen een _key, value pair_ genoemd.

### File Input/Output
Stel dat je `bericht.txt` wilt inlezen. Dat gaat als volgt:

{% highlight ruby %}
contents = File.read('bericht.txt')
{% endhighlight %}

`contents` is nu een (hele lange) string.

Naar bestanden schrijven kan ook.

{% highlight ruby %}
file = File.open("test.txt", "w")
file.write("hallo!")
file.close
{% endhighlight %}

### Ruby Documentation
Nu jullie een aantal basisbegrippen hebben leren kennen, moeten jullie de documentatie van de ruby-taal leren lezen. Ook wij zoeken nog dagelijks dingen op.

* [http://www.ruby-doc.org/core-1.9.3/String.html](http://www.ruby-doc.org/core-1.9.3/String.html)
* [http://www.ruby-doc.org/core-1.9.3/Array.html](http://www.ruby-doc.org/core-1.9.3/Array.html)
* [http://www.ruby-doc.org/core-1.9.3/Hash.html](http://www.ruby-doc.org/core-1.9.3/Hash.html)

De volgende functies kunnen van pas komen: 

* `String#split`
* `Array#join` 

`String#split` betekent: de functie `split` die hoort bij `String`. Gebruik de bovenstaande documentatie (of gebruik google) om uit te vinden hoe je `split` en `join` gebruikt.

##De opdracht

###De functie `build_hash`

In deze opdracht ga je computer inzetten om berichten snel te versleutelen en weer te ontcijferen. Hiervoor zul je een aantal functies moeten schrijven. Begin bij een functie `build_hash`, die met een gegeven 'shift' (het aantal plaatsen dat elke letter moet worden verschoven) een hash aanmaakt.  
In deze hash moet elke letter in het alfabet gekoppeld worden aan de letter waar hij door vervangen moet worden. We vatten de spatie `" "` op als 27e letter. Een shift van 3 zou moeten opleveren:

{% highlight ruby %}

{"a"=>"d", "b"=>"e", "c"=>"f", "d"=>"g", "e"=>"h", "f"=>"i", "g"=>"j", "h"=>"k", "i"=>"l", "j"=>"m", "k"=>"n", "l"=>"o", "m"=>"p", "n"=>"q", "o"=>"r", "p"=>"s", "q"=>"t", "r"=>"u", "s"=>"v", "t"=>"w", "u"=>"x", "v"=>"y", "w"=>"z", "x"=>" ", "y"=>"a", "z"=>"b", " " => "c"}

{% endhighlight %}

Je ziet hier dat de "a" drie plaatsen is opgeschoven en in het gecodeerde bericht een "d" wordt. 

###De functie `encrypt`

Dit is de functie waar het allemaal om draait. Als je deze functie een bericht en een bepaalde shift geeft, zou het de build_hash functie moeten aanroepen en dan vervolgens het bericht letter *voor* letter (denk hierbij aan een `for`loop) moeten coderen tot een rij tekst waar je niks zinnigs meer in ziet.

###De functie `decrypt`

Als je iets codeert, wil je het natuurlijk ook weer terug kunnen vertalen. Hiervoor heb je deze functie nodig. We gaan er hier van uit dat je de 'sleutel' (dus de shift) weet. Denk goed na, je hoeft hiervoor niet veel nieuwe code te schrijven!

##Het bestand ontcijferen

Je hebt nu alles gemaakt om het bestand `encrypted_message.txt` te gaan ontcijferen. Lees het bestand in, draai het in zijn geheel door de `decrypt` functie en sla het ontcijferde stuk tekst op in `decrypted_message.txt`.

### (Extra) Leestekens

Je programma kan nu allerlei stukken tekst, zo lang als je maar wilt, versleutelen en weer decoderen. Maar je zult merken dat het niet meer werkt wanneer er andere tekens, zoals `; , . ! ?` in voor komen. Probeer een manier te bedenken om dit probleem te omzeilen en schrijf in `cipher_test.rb` een extra test om dit te testen.

### (Extra) Kraken zonder shift

Nu gaan jullie een bericht ontcijferen! Hoe zou je dit doen?

Je kunt alle mogelijkheden langsgaan. Deze methode heet Brute Force. Of is er een slimmere manier?

Probeer nu bestand `encrypted.txt` te kraken. Je mag hierbij gebruik maken van de woordenlijst die in de map staat. Denk goed na. Hoe weet de computer dat hij de juiste shift te pakken heeft? Veel succes!
