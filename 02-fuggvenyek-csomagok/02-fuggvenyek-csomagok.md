# Eml�keztet� #

## K�rd�sek ##
1. Milyen elnevez�si konveci�t haszn�lunk csomagokra?
2. Mi a kapcsolat a csomag �s a f�jlrendszeren elhelyezked� mappaszerkezet k�z�tt?
2. Milyen l�that�s�gi m�dos�tokkal tal�lkozt�l?
3. Mit nevez�nk a f�ggv�ny szignat�r�j�nak?
4. T�lterhelhet�-e a f�ggv�ny a visszat�r�si �rt�k�re n�zve?
5. Milyen param�ter�tad�si m�d(ok) vannak?
6. Hogy haszn�lunk m�sik csomagban l�v� oszt�lyokat?
7. Mit jelent az `import pkg.*;`?
8. Rekurz�v-e az `import`?
9. Csak statikus met�dusokat �s mez�ket szeretn�nk import�lni, milyen lehet�s�g�nk van?
10. Mi t�rt�nik, ha egy adott n�ven k�t oszt�ly is szerepel k�l�nb�z� csomagokban, �s mind a kett�t import�ljuk? Hogy oldjuk meg a probl�m�t?

## K�rnyezet be�ll�t�sa ##
Eml�keztet�:

``` dos
	Microsoft Windows XP [verzi�sz�m: 5.1.2600]
	(C) Copyright 1985-2001 Microsoft Corp.
	
	c:\tmp>set PATH=%PATH%;c:\Program Files\Java\jdk1.6.0_12\bin\
	
	c:\tmp>javac -version
	javac 1.6.0_12
	
	c:\tmp>javac HelloWorldApp.java
	
	c:\tmp>java HelloWorldApp
	Hello World!
	
	c:\tmp>
```

# Csomagok #
Modulariz�ci�, n�v�tk�z�sek felold�sa, hozz�f�r�s szab�lyoz�s, etc. (mint a
C++ namespace). Oszt�lyok, interf�szek gy�jtem�nye. Haszn�lhat� a `*` wildcard.
Alap�rtelmezetten l�tszik a `java.lang.*` csomag minden eleme, minden m�st
import�lni kell (an�lk�l �n. _fully qualified classname_ seg�ts�g�vel
hivatkozhatunk, pl. `java.util.Vector`): 

``` java
import java.util.Vector;	// 1 tipushoz  
import java.math.*;			// Minden package-beli tipus lathatova valik  
	  
import java.awt.*;			// GUI  
import java.awt.event.*;	// GUI - esemenykezeles  
import javax.swing.*;		// Advancedebb GUI  
import java.util.*;			// Adatstrukturak  
import java.io.*;			// IO  
import java.util.regex.*;	// Regexp  
	  
// static import: minden static konstans lathato az adott osztalybol  
// fenntartasokkal hasznalni  
import static java.lang.Math.*;  
```

A ford�t�s neh�zkes, nincs rekurz�v `javac -R *.java`. Lek�pez�s a
f�jlrendszerre: minden `.` karakterrel szepar�lt r�sz egy k�nyvt�rat jelent,
ford�t�s a gy�k�rk�nyvt�rb�l t�rt�nik. Static importot csak offtosan
(struktur�lts�g, enkapszul�ci�, egys�gbez�r�s ellen hat - haszn�ljatok helyette
dedik�lt oszt�lyt vagy interf�szt). Csomag defin�ci�ja a Java f�jl legelej�n:

``` java
package pkg;
	
// Import utasitasok
	
public class HelloWorldApp {
    public static void main(String args[]) {
        System.out.println("Hello World!");
    }
};
```

> **Fontos** Ha csomagokat haszn�lunk, akkor mindig a *package root* al�l adjuk ki a ford�t�shoz/futtat�shoz sz�ks�ges parancsokat (azaz abb�l a k�nyvt�rb�l, ami a legfels� szint� csomagokat tartalmazza)! Erre az�rt van sz�ks�g, mert ha nem �ll�tod be k�zzel a `CLASSPATH` v�ltoz� �rt�k�t (ez azon �tvonal, ahol a Java alap�rtelmez�s szerint keresi a sz�ks�ges oszt�lyokat), akkor az a `.` (azaz az aktu�lis) k�nyvt�r. �gy ha pl. a `foo.A` oszt�ly hivatkozik egy `foo.bar.B` oszt�lyra, �s a `foo` k�nyvt�rb�l ford�tod az `A` oszt�lyt, akkor a ford�t�/futtat�k�rnyezet a `foo` konyvt�rban keres egy m�sik `foo`, majd abban egy `bar` k�nyvt�rat!
> 
> Teh�t a l�nyeg: **mindig a package root k�nyvt�rb�l ford�tsunk, futtassunk!**

**Ford�t�s** a Java f�jl **teljes �tvonal�nak** megad�s�val:

	C:\tmp>javac pkg/HelloWorldApp.java

**Futtat�shoz** azonban a **teljes hivatkoz�si n�v** sz�ks�ges (*fully qualified classname*):
	
	C:\tmp>java pkg.HelloWorldApp
	Hello World!

Ha esetleg n�v�tk�z�s van (2 azonos nev� oszt�ly), akkor min�s�tett n�vvel
�rhetj�k el az egyiket (pl. `java.util.List`, `java.awt.List`). Importokat
haszn�ljatok nyugodtan, nem g�z, nem em�szt er�forr�st (nem C++, dinamikus
oszt�lybet�lt�s van).


## Rekurz�v ford�t�s ##
Alapb�l nincs rekurz�v ford�t�s, viszont megadhat� a ford�t�nak egy f�jl,
ami a ford�tani k�v�nt f�jlok list�j�t tartalmazza - ezt a `@` karakterrel
jelezheted.

	# Linux
	$ find -name "*.java" > sources.txt
	$ javac @sources.txt

	:: Windows
	> dir /s /B *.java > sources.txt
	> javac @sources.txt

> **R�szletesen** [Itt](http://stackoverflow.com/questions/6623161/javac-option-to-compile-recursively/8769536#8769536)

# F�ggv�nyek #
�ltal�nos protot�pus:

	<m�dos�t�szavak> <visszat�r�si �rt�k> <n�v>( <param�terek list�ja> )
	        [ throws <kiv�tel lista> ] {
	    <utas�t�s1>;
	    <utas�t�s2>;
	    ...
	}

Param�ter �tad�s �rt�k szerint t�rt�nik (m�g a referenci�k is!).

* M�dos�t�szavak:
	* L�that�s�g: `public`, `protected`, `private`. Ha nem defini�lt, akkor �n.
	  *default* / _package-private_ / *package-level* l�that�s�g.
	* Lehet `abstract`: ekkor nincs implement�ci� (mint a C++ _pure virtual_
	  f�ggv�nyei) lesz�rmazottban k�telez�en fel�ldefini�land�
	* Lehet `final`: fel�ldefini�lhat�s�g letilt�s�ra
	* Lehet `static`: oszt�ly szint� f�ggv�ny (**Fontos:** static kontextusb�l
	  csak static m�dos�t�val ell�tott hivatkoz�s szerepelhet)
	* Egy�b, pl. `strictfp`, `native`, `synchronized`, `transient`, `volatile`
	  (ut�bbi kett� **csak** fieldekre). Ezekr�l k�s�bb.
* Visszat�r�si �rt�k szerinti csoportos�t�s:
	* `void`: elj�r�s
	* Minden egy�b: f�ggv�ny
* Met�dusn�v: _lowerCamelCase_ form�tumban
* Param�ter �tad�s: minden param�ter �rt�k szerint ad�dik �t
_m�g a referenci�k is_.

**Szignat�ra** a f�ggv�ny neve �s param�tereinek t�pusa -- m�s **nem**. P�ld�ul:

``` java
eredmenyMeghatarozasa( double, int, int )
```

Overloading, overriding.

# +/- Feladatok #

A feladatokat a `gyak2.f1` ill. `gyak2.f2`, ... csomagba rakj�tok!

### Faktori�lis ###
�rjatok programot, mely kisz�m�tja a param�ter�l kapott sz�m faktori�lis�t.

``` java
    class F1 {
        public static void main(String[] args) {
            System.out.println(fakt(5));
        }
        
        public static int fakt(int n) {
            int res = 1;
            for (int i = 1; i < n; ++i) {
                res *= i;
            }
            return res;
        }
    }
```

### Rekfakt ###
�rj faktori�list megold� programot, melyben a f�ggv�ny rekurz�v.

``` java
    class F2 {
        public static void main(String[] args) {
            System.out.println(fakt(5));
        }
        
        public static int fakt(int n) {
            if( n == 0 ) {
                return 1;
            } else {
                return n * fakt(n-1);
            }
        }
    }
```

### Fib ###
Add �ssze az �sszes p�ratlan r�sz-fibonacci sz�mot eg�szen addig, am�g az adott r�sz-fibonacci sz�m �rt�ke nem �ri el 400000.

### Euclid ###
K�sz�tsetek egy f�ggv�nyt, amely az Euklideszi-algoritmus alapj�n meghat�rozza
k�t sz�m legnagyobb k�z�s oszt�j�t! Az algoritmus pszeudok�dja:

	function gcd(a, b)  
	    if a = 0  
	       return b  
	    while b != 0  
	        if a > b  
	           a := a - b  
	        else  
	           b := b - a  
	    return a  

K�sz�tsd el a f�ggv�ny rekurz�v v�ltozat�t is!

### Quadratic ###
K�sz�tsetek egy f�ggv�nyt, amely megadja egy m�sodfok� egyenlet gy�keit! A
f�ggv�ny defin�ci�ja legyen a k�vetkez�:

``` java
private static double[] sqroots(final double a, final double b, final double c) {
	// ...
}
```

A f�ggv�ny visszat�r�si �rt�ke legyen:

* �res t�mb (nem `null` �rt�k!), ha `a == 0` vagy a diszkrimin�ns negat�v,
* egyelem� t�mb, ha egyetlen megold�s van (`D == 0`), illetve
* k�telem� t�mb, amennyiben k�t k�l�nb�z� megold�s l�tezik!

A param�tereket a parancssori argumentumok hat�rozz�k meg, amiket a
`Double.parseDouble()` seg�ts�g�vel tudsz �rtelmezni.
