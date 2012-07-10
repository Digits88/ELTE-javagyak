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
  * Dean Wampler, Alex Payne: [Programming Scala][programming-scala]

# Feladatok #

Megjegyz�sek:

* Az al�bbi feladatok f�k�nt [Phil Gold][phil] [S-99: Ninety-Nine Scala Problems][s99] �r�s�n alapszanak, amely val�j�ban Werner Hett (Berne University of Applied Sciences) [Ninety-Nine Prolog Problems][p99] m�v�nek egy adapt�ci�ja. Ha a feladatok t�l nehezek, k�nny�ek, esetleg kev�sb� izgalmasak, a fenti oldalakon b�ven tal�lhat�k alternat�v�k.

## K�nnyebb feladatok ##

### Lista els� elem�nek meghat�roz�sa ###

K�sz�ts egy f�ggv�nyt a k�vetkez� szignat�r�val:

```scala
def lastRecursive[A](n: Int, ls: List[A]): A
```

P�lda a haszn�latra:

```scala
scala> last(List(1, 1, 2, 3, 5, 8))
res0: Int = 8
```

A megval�s�t�shoz ne a be�p�tett f�ggv�nyt haszn�ld, hanem pr�b�ld a `match`, `::` oper�tor �s �res lista (`Nil`) seg�ts�g�vel megoldani a feladatot!

### Lista v�g�t�l sz�m�tott N-edik elem meghat�roz�sa ###

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
scala> lastNth(2, List(1, 1, 2, 3, 5, 8))
res0: Int = 5
```

A megval�s�t�shoz ne a be�p�tett f�ggv�nyt haszn�ld, hanem vagy k�sz�ts egy v�gz�d�s szerinti rekurzi�t (*tail recursion*), vagy haszn�ld valamely `fold()` f�ggv�nyt!

### Stringek nagybet�ss� alak�t�sa ###

K�sz�ts egy f�ggv�nyt, amely tetsz�leges sz�m� String param�tert elfogad (nem list�t!), �s minden param�tert nagybet�ss� alak�t!

P�lda a haszn�latra:

```scala
scala> Upper.upper("A", "First", "Scala", "Program"))
res0: Array(A, FIRST, SCALA, PROGRAM)
```

A f�ggv�nyt tedd egy megfelel� `object` defin�ci�ba, valamint haszn�ld a megold�shoz a `_` alap�rtelmezett param�terjel�l�st!

### String lista �sszef�z�se egyetlen Stringg� ###

```scala
def joiner(strings: List[String], separator: String): String
```

A separator param�ter alap�rtelmezett �rt�kkel is rendelkezzen, ez legyen a sz�k�z karakter!

P�lda a haszn�latra:

```scala
scala> joiner(List("Programming", "Scala"))
res0: String = "Programming Scala"
```

### Stringek p�ros�t�sa a hosszukkal ###

```scala
def sizes(ls: List[String]): List[(Int, String)]
```

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

String list�ra 

```scala
scala> minOf(List(1,2,3))
res9: Int = 1

scala> maxOf(List(1,2,3))
res9: Int = 3
```

## K�zepesen neh�z feladatok ##

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

Caesar...

## Neh�z feladatok ##

### Java k�nyvt�rak haszn�lata ###

T�ltsd le az [iText][itext] k�nyvt�rat, amely egy standard Java k�nyvt�r. Haszn�ld az API-t Scalab�l, �s k�sz�ts egy egyszer� PDF form�tum� f�jlt a seg�ts�g�vel!

Egy egyszer� [tutorial][itext-tutorial], amely a haszn�latot mutatja.

A program a k�sz�tett PDF tartalm�t olvassa egy f�jlb�l!

### N-kir�lyn� probl�ma ###


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
  [itext]: 		http://itextpdf.com
  [itext-tutorial]: 	http://itextpdf.com/examples/iia.php?id=12
  [code-jam]:		http://code.google.com/codejam/contest/1460488/dashboard

