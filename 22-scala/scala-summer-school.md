# Seg�danyagok#

* Az el�ad�s anyagai let�lthet�k az al�bbi linken: [xxx.tgz][scala-ea]
* Fejleszt�k�rnyezet let�lt�se
  * Scala IDE, valamint a sz�ks�ges Java futtat�k�rnyezet egyben let�lthet� az al�bbi linken: [xxx.tgz][scala-ide]
  * A fejleszt�k�rnyezetr�l tov�bbi inform�ci� az al�bbi oldalon tal�lhat�: http://scala-ide.org/
* Scala weboldala: http://www.scala-lang.org/
* K�z�ss�gi Scala dokument�ci�s project (tutorialok, Scala Improvement Process, Language Specification, stb.): http://docs.scala-lang.org/
* Scaladoc online b�ng�szhet�, legfrissebb v�ltozata: http://www.scala-lang.org/api/current/index.html

* Aj�nlott olvasm�nyok (igyenesen el�rhet� k�nyvek):
  * Joshua D. Suereth: [Scala in Depth][scala-in-depth]
  * Cay S. Horstmann: [Scala for the Impatient][scala-impatient]
  * Dean Wampler, Alex Payne: [Programming Scala][oreilly-scala]

# Feladatok #

Megjegyz�sek:

* Az al�bbi feladatok f�k�nt [Phil Gold][phil]: [S-99 - Ninety-Nine Scala Problems][s99] �r�s�n alapszanak, amely val�j�ban Werner Hett (Berne University of Applied Sciences) [Ninety-Nine Prolog Problems][p99] m�v�nek egy adapt�ci�ja. Ha a feladatok t�l nehezek, k�nny�ek, esetleg kev�sb� izgalmasak, a fenti oldalakon b�ven tal�lhat�k alternat�v�k.

## K�nnyebb feladatok ##

Az al�bbiakban egyszer�bb feladatok tal�lhat�k, amelyek nagyj�b�l 15-20 perc alatt megoldhat�k. Az els� feladatokn�l m�g konkr�t szignat�r�t is megadunk, k�s�bb azonban ezt fokozatosan elhagyjuk, ezt is nektek kell helyesen meg�rnotok.

### Lista els� elem�nek meghat�roz�sa ###

K�sz�ts egy f�ggv�nyt a k�vetkez� szignat�r�val:

```scala
def last[A](n: Int, ls: List[A]): A
```

P�lda a haszn�latra:

```scala
scala> last(List(1, 1, 2, 3, 5, 8))
res0: Int = 8
```

A megval�s�t�shoz ne a be�p�tett f�ggv�nyt haszn�ld, hanem pr�b�ld a `match`, `::` oper�tor �s �res lista (`Nil`) seg�ts�g�vel megoldani a feladatot!

### Lista v�g�t�l sz�m�tott N. elem meghat�roz�sa ###

K�sz�ts egy f�ggv�nyt a k�vetkez� szignat�r�val:

```scala
def lastNth[A](n: Int, ls: List[A]): A
```

P�lda a haszn�latra:

```scala
scala> lastNth(2, List(1, 1, 2, 3, 5, 8))
res0: Int = 5
```

A megval�s�t�shoz ne a be�p�tett f�ggv�nyt haszn�ld, hanem adj egy rekurz�v algoritmust r�!

### Lista hossz�nak meghat�roz�sa ###

K�sz�ts egy f�ggv�nyt a k�vetkez� szignat�r�val:

```scala
def length[A](ls: List[A]): Int
```

P�lda a haszn�latra:

```scala
scala> length(List(1, 3, 5, 7))
res0: Int = 4
```

A megval�s�t�shoz ne a be�p�tett f�ggv�nyt haszn�ld, hanem vagy k�sz�ts egy v�gz�d�s szerinti rekurzi�t (*tail recursion*), vagy haszn�ld valamely `fold()` f�ggv�nyt!

### Stringek nagybet�ss� alak�t�sa ###

K�sz�ts egy f�ggv�nyt, amely tetsz�leges sz�m� String param�tert elfogad (*nem list�t!*), �s minden param�tert nagybet�ss� alak�t!

A f�ggv�nyt tedd egy megfelel� `object` defin�ci�ba, valamint haszn�ld a megold�shoz a `_` alap�rtelmezett param�terjel�l�st!

P�lda a haszn�latra:

```scala
scala> Upper.upper("A", "First", "Scala", "Program"))
res0: Array(A, FIRST, SCALA, PROGRAM)
```

### String lista �sszef�z�se egyetlen karakterl�ncc� ###

K�sz�ts egy f�ggv�nyt a k�vetkez� szignat�r�val:

```scala
def joiner(strings: List[String], separator: String): String
```

A separator param�ter alap�rtelmezett �rt�kkel is rendelkezzen, ez legyen a sz�k�z karakter (*ehhez a megadott szignat�r�t is m�dos�thatod, ha sz�ks�ges*)!

P�lda a haszn�latra:

```scala
scala> joiner(List("Programming", "Scala"))
res0: String = "Programming Scala"
```

### Stringek p�ros�t�sa a hosszukkal ###

K�sz�ts egy f�ggv�nyt a k�vetkez� szignat�r�val, amely egy String list�hoz visszaad olyan p�rokat, amelyek tartalmazz�k az adott Stringet valamint annak a hozssz�t:

```scala
def sizes(ls: List[String]): List[(Int, String)]
```

P�lda a haszn�latra:

```scala
scala> sizes(List("a", "bc", "def"))
res0: List[(Int, String)] = List((1,a), (2,bc), (3,def))
```

### Folding ###

K�sz�tsd el a k�vetkez� f�ggv�nyek defin�ci�it, amelyekhez haszn�ld valamelyik `fold()` f�ggv�nyt!

```scala
// Elemek osszege
def sum(list: List[Int]): Int

// Elemek szorzata
def product(list: List[Int]): Int

// Elemek szama
def count(list: List[Any]): Int

// Elemek atlaga
def average(list: List[Double]): Double
```

### Reducing ###

K�sz�tsd el a k�vetkez� f�ggv�nyek defin�ci�it, amelyekhez haszn�ld valamelyik `reduce()` f�ggv�nyt!

```scala
// Legkisebb elem meghatarozasa
scala> minOf(List(1,2,3))
res0: Int = 1

// Legnagyobb elem meghatarozasa
scala> maxOf(List(1,2,3))
res0: Int = 3
```

## K�zepesen neh�z feladatok ##

Az al�bbi feladatok m�r kicsit bonyolultabbak, az el�ad�s anyag�nak akt�v tanulm�nyoz�sa sz�ks�ges a megold�sukhoz.

### Companion objektumok ###

K�sz�ts egy egyszer� `Pair` oszt�lydefin�ci�t, amely String p�rok el��ll�t�s�ra alkalmazhat�! Ennek egyetlen f�ggv�nye legyen:

```scala
def value(): String
```

Amely egy `new Pair("key", "value")` eset�n adja vissza a `"key = value"` karakterl�ncot!

K�sz�ts tov�bb� egy *companion objektumot* is az oszt�lydefin�ci�hoz, amely tegye lehet�v� a k�vetkez� haszn�latot:

```scala
val p = Pair("a", "b") // Nota bene: Nem szerepel 'new' operator!
```

### Karakterkombin�ci�k el��ll�t�sa ###

K�sz�ts egy olyan f�ggv�nyt, amely a megadott String karaktereinek minden lehets�ges permut�ci�j�t el��ll�tja!

P�lda a haszn�latra:

```scala
scala> perm("abc")
res0: List[String] = List("abc", "acb", "bac", "bca", "cab", "cba")
```

### Egybe�gyazott list�k kiegyenes�t�se ###

```scala
scala> flatten(List(List(1, 1), 2, List(3, List(5, 8))))
res0: List[Any] = List(1, 1, 2, 3, 5, 8)
```

A megval�s�t�shoz haszn�ld a `flatMap()` f�ggv�nyt!

### Euklideszi algoritmus ###

```scala
scala> gcd(36, 63)
res0: Int = 9
```

A megval�s�t�shoz haszn�ld az euklideszi algoritmust!

### Relat�v pr�mek ###

D�nts�k el k�t sz�mr�l, hogy relat�v pr�mek-e!

```scala
scala> 35.isCoprimeTo(64)
res0: Boolean = true
```

**Megjegyz�s** Vegy�k �szre, hogy a f�ggv�nyt a fenti m�don egy tetsz�leges sz�mon h�vjuk!

### Mintailleszt�s regul�ris kifejez�sekkel ###

Legyen adott a k�vetkez� lista defin�ci�:

```scala
val catalog = List(
  "Book: title=Programming Scala, authors=Dean Wampler, Alex Payne",
  "Magazine: title=The New Yorker, issue=January 2009",
  "Book: title=War and Peace, authors=Leo Tolstoy",
  "Magazine: title=The Atlantic, issue=February 2009",
  "BadData: text=Who put this here??"
)
```

A lista bej�r�sa sor�n �rjuk ki a k�perny�re minden k�nyv (�s csak azok!) c�m�t, valamint �r�j�t (de csak azokat!). A megold�shoz haszn�ljunk mintailleszt�st regul�ris kifejez�sekre!

### K�dol�s ###

K�sz�ts�nk egy nagyon egyszer� monoalfabetikus (egy karaktert mindig ugyanazzal a m�sik karakterrel helyettes�t�) k�dol� rendszert, amelyet maga Caesar is haszn�lt! A k�dol�s l�nyege, hogy minden karaktert a t�le h�rom karakterrel jobbra szerepl�vel �br�zolunk.

P�lda:

```scala
scala> encode("Alea iacta est")
res0: String="dohd ldfwd hvw"
```

K�dol�s el�tt minden karaktert alak�tsunk kisbet�ss�, valamint el�g csup�n az angol ABC karaktereivel foglalkozni!

R�szletek a k�dol�s t�rt�net�r�l a [Wikip�di�ban][caesar].

## Neh�z feladatok ##

Az al�bbi feladatok m�r esetleg n�mi ut�naj�r�st vagy komolyabb gondolkodni val�t jelentenek.

### Java k�nyvt�rak haszn�lata ###

T�ltsd le az [iText][itext] k�nyvt�rat, amely egy standard Java k�nyvt�r. Haszn�ld az API-t Scalab�l, �s k�sz�ts egy egyszer� PDF form�tum� f�jlt a seg�ts�g�vel!

Egy egyszer� [tutorial][itext-tutorial], amely a haszn�latot mutatja.

A program a k�sz�tett PDF tartalm�t olvassa egy f�jlb�l!

### A lovag �tja ###

Adott egy `NxN` m�ret� sakkt�bla. L�tezik-e olyan l�p�ssorozat, amely sor�n egy l� b�b�val minden sakkt�bla mez�t �rinthet�nk egy megadott kezd�pontr�l indulva?

**Tov�bbfejleszt�si lehet�s�g** L�tezik-e ugyanilyen *z�rt �t* (z�rt �t egy olyan �t, amely sor�n az utols� l�p�sben visszat�r�nk a kezd�poz�ci�ra)?

R�szletek a probl�m�r�l [Wikip�di�ban][knights-tour].

### Google Code Jam feladatok ###

Ha kicsit izgalmasabb feladatokat szeretn�l, az al�bbi weboldalon [a hivatalos Google Code Jam selejtez� feladatait][code-jam] is megpr�b�lhatod ;-)

  [scala-ea]: 		http://
  [scala-ide]: 		http://...
  [oreilly-scala]: 	http://ofps.oreilly.com/titles/9780596155957/
  [scala-impatient]: 	http://typesafe.com/resources/scala-for-the-impatient
  [scala-in-depth]: 	http://typesafe.com/resources/scala-in-depth
  [phil]: 		http://aperiodic.net/phil/
  [p99]: 		https://prof.ti.bfh.ch/hew1/informatik3/prolog/p-99/
  [s99]: 		http://aperiodic.net/phil/scala/s-99/
  [caesar]: 		http://en.wikipedia.org/wiki/Caesar_cipher
  [itext]: 		http://itextpdf.com
  [itext-tutorial]: 	http://itextpdf.com/examples/iia.php?id=12
  [knights-tour]: 	http://en.wikipedia.org/wiki/Knight's_tour
  [code-jam]:		http://code.google.com/codejam/contest/1460488/dashboard

