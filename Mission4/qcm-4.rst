.. Copyright |copy| 2013 by Olivier Bonaventure
.. raw:: html

  <link href="css/prettify.css" type="text/css" rel="stylesheet" />
  <script type="text/javascript" src="js/jquery-1.7.2.min.js"></script>
  <script type="text/javascript" src="js/jquery-shuffle.js"></script>
  <script type="text/javascript" src="js/prettify.js"></script>
  <script type="text/javascript" src="js/rst-form.js"></script>
  <script type="text/javascript">$nmbr_prop = 4</script> 



================================================
Mission 4. Manipulation de cha�nes de caract�res
================================================


Ces questions supposent que vous avez lu les sections suivantes du livre de r�f�rence |jn|_ 

 - |jn2.3|_

   - |jn2.3.1|_
   - |jn2.3.2|_
   - |jn2.3.3|_ n'est pas vu dans le cadre de ce cours

 - |jn4.7|_

   - |jn4.7.1|_
   - |jn4.7.2|_
   - |jn4.7.3|_


Les sections vues pr�c�demment restent bien entendu d'actualit�.

Question 1. Port�e des variables
--------------------------------


En Java, une d�claration de variable a comme port�e la zone qui s�pare la d�claration de la variable de la fin du bloc dans lequel elle appara�t. Une r�gle de bonne pratique est de d�clarer chaque variable au d�but du bloc de la m�thode dans laquelle elle est utilis�e ou dans un bloc d'une boucle par exemple. Consid�rons la m�thode d�finie comme suit ::

    public static void showScope (int a, double r)
    { 
      int j;
      ... // ligne a
      for (int i = 0; ... ) {
	  double y;
	  ... // ligne c
	  if(i>0) {
	     boolean b;
	     ... // ligne e
	  }
      }
      ... // ligne f

    }


Les propositions ci-dessous sont relatives � des instructions plac�es � certains lignes identifi�es ci-dessus. Laquelle de ces propositions est-elle correcte ?

.. class:: positive

-
 ::
 
   System.out.print(a); // ligne a
   System.out.print(r); // ligne c
   System.out.print(b); // ligne e
   System.out.print(j); // ligne f   

-
 ::
 
   System.out.print(j); // ligne a
   System.out.print(y); // ligne c
   System.out.print(b); // ligne e
   System.out.print(a); // ligne f   

.. class:: negative

-
 ::
 
   System.out.print(a); // ligne a
   System.out.print(y); // ligne c
   System.out.print(b); // ligne e
   System.out.print(i); // ligne f   

 .. class:: comment

    La variable ``i`` n'est utilisable qu'� l'int�rieur de la boucle ``for``. Elle ne peut pas �tre utilis�e en dehors de cette boucle.

-
 ::

   System.out.print(i); // ligne a
   System.out.print(y); // ligne c
   System.out.print(b); // ligne e
   System.out.print(i); // ligne f   

 .. class:: comment

    La variable ``i`` n'est utilisable qu'� l'int�rieur de la boucle ``for``. Elle ne peut pas �tre utilis�e en dehors de cette boucle.


-
 ::

   System.out.print(a); // ligne a
   System.out.print(i); // ligne c
   System.out.print(r); // ligne e
   System.out.print(y); // ligne f   

 .. class:: comment

    La variable ``y`` n'est utilisable qu'apr�s sa d�claration dans le bloc ``for``. En dehors de ce bloc, elle ne peut pas �tre utilis�e. 



Question 2. Port�e des variables
--------------------------------

Parmi les d�finitions de m�thodes ci-dessous, quelle est celle qui affichera correctement ``2012`` � l'�cran ?


.. class:: positive

-
 ::

   public static void main(String[] args) {
   
     int i=2011;
     int b=1;
     if(b==1) {
        i=b;
     }
     else {
        i++;
     }
     System.out.println(i);

   }

 .. class:: comment

    Dans cette m�thode, ``b`` vaut ``1`` et donc le bloc ``else`` est ex�cut� et la valeur de ``i`` est incr�ment�e.

-
 ::

   public static int f(int b) {
     for(int i=1;i<10;i=i+1) {
      b=b+i;
     }

     return b;
   }  

   public static void main(String[] args) {
   
     int i=2012;
     int b=1;
     b=f(i);
     System.out.println(i);

   }

 .. class:: comment 

    Notez que la variable ``i`` d�clar�e dans la m�thode ``f`` est diff�rente de la variable ``i`` d�clar�e dans la m�thode ``main``.

.. class:: negative

-
 ::

   public static void main(String[] args) {
   
     int i=2012;
     int b=1;
     if(b==0) {
        int i=1;
     }
     else {
     	i=1234;
     }
     System.out.println(i);

   }

 .. class:: comment

    ``javac`` refuse de compiler ce code car on cherche � d�clarer deux fois la variable ``i`` ce qui est interdit dans la m�me m�thode.


-
 ::

   public static void main(String[] args) {
   
     int i=2012;
     int b=1;
     for(i=1; i<10; i=i+1) {
        b=b+i;
     }
     System.out.println(i);

   }

 .. class:: comment

    Cette m�thode ``main`` modifie la valeur de la variable ``i`` dans la boucle ``for``. La valeur affich�e est ``10``. 

-
 ::

   public static void main(String[] args) {
   
     int i=2012;
     int b=1;
     while(b!=0) {
       i=i+1;
       b=b-1;
     }
     System.out.println(i);

   }

 .. class:: comment

    Cette m�thode ``main`` met � jour la variable i dans le bloc ``while``. C'est donc 2013 qui est affich�. 



-
 ::

   public static void main(String[] args) {
   
     int i=2012;
     int b=1;
     if(b!=0) {
       i=i+1;
       b=b-1;
     }
     else {
       i=2012;
     }

     System.out.println(i);

   }

 .. class:: comment

    Cette m�thode ``main`` met � jour la variable i dans le bloc ``if``. C'est donc 2013 qui est affich�. 



Question 3. Surcharge de m�thodes
---------------------------------


En Java, il est possible de d�finir plusieurs m�thodes qui ont le m�me nom pour autant qu'elles diff�rent par le nombre ou le type de leurs arguments. La m�thode ``System.out.print`` par exemple est une m�thode qui existe avec comme argument un entier, un caract�res, une cha�ne de caract�res, un bool�en. Consid�rons les d�clarations de m�thodes ci-dessous :: 


 public static void affiche(char c, int i) {
  System.out.println("char, int");
 }

 public static void affiche(int i, int j) {
  System.out.println("int, int");
 }

 public static void affiche(String s, double j) {
  System.out.println("String, double");
 }

 public static void affiche(String s, boolean b) {
  System.out.println("String, boolean");
 }

Laquelle des s�quences d'invocation suivantes affiche � l'�cran ::

  char, int
  String, double
  int, int
  String, boolean


.. class:: positive

- 
 ::
   
   affiche('0',-4);
   affiche("abc",3.23);
   affiche(0,0);
   affiche("3.12",false);

- 
 ::
   
   affiche('c',0);
   affiche("3.12",3.23);
   affiche(-1,1);
   affiche("abc",false);


.. class:: negative

- 
 ::
   
   affiche('c',-2);
   affiche("abc",3.23);
   affiche(2,8);
   affiche("abc","true");

 .. class:: comment
 
    La derni�re ligne appelle une m�thode qui prend comme arguments deux ``String`` et non un ``String`` et un ``boolean``

- 
 :: 
   
   affiche('8',-2);
   affiche(3.12,3.231);
   affiche(3,-12);
   affiche("3.1",false);

 .. class:: comment

    La deuxi�me ligne appelle une m�thode qui prend comme arguments deux ``double`` et non un ``String`` et un ``double``.

-
 ::
    
   affiche("8",-2);
   affiche("3.12",3.231);
   affiche(6,-2);
   affiche("true",false);

 .. class:: comment

    La premi�re ligne appelle une m�thode qui prend comme arguments un ``String`` et un ``int`` et non un caract�re et un ``int``.


-
 ::
    
   affiche('7',0);
   affiche("3.12",3.231);
   affiche(6,"-2");
   affiche("false",true);

 .. class:: comment

    La troisi�me ligne appelle une m�thode qui prend comme arguments un ``int`` et un ``String`` et non deux ``int``.

Question 4. Conversion de types
-------------------------------

En Java, il existe diff�rentes solutions pour convertir un nombre r�el en un nombre entier. Consid�rons la variable ``p`` d�clar�e comme suit ::


	double p=3.84;

Laquelle des instructions ci-dessous affiche-t-elle ``3`` � l'�cran ?

.. class:: positive

-
 ::

 	System.out.println((int) p);

 .. class:: comment

    En Java, ``(int) p`` permet de convertir le contenu de la variable ``p`` en une valeur enti�re. 

.. class:: negative

-
 ::

	System.out.println(Math.round(p));

 .. class:: comment

    La m�thode ``Math.round`` retourne la valeur arrondie. Dans ce cas, le r�sultat est ``4``. Voir http://docs.oracle.com/javase/7/docs/api/java/lang/Math.html#round(double)
-
 ::

	System.out.println(p);

 .. class:: comment

    Cette instruction affiche la valeur de ``p``, c'est-�-dire ``3.84``. 

-
 ::

	System.out.println(Math.ceil(p));

 .. class:: comment

    La m�thode  ``Math.ceil`` retourne un ``double`` et non un entier. L'instruction affiche ``4.0`` � l'�cran. Voir http://docs.oracle.com/javase/7/docs/api/java/lang/Math.html#ceil(double)

-
 ::

	System.out.println(Math.floor(p));

	
 .. class:: comment

    La m�thode ``Math.floor`` retourne un ``double`` et non un entier. L'instruction affiche ``3.0`` � l'�cran. Voir http://docs.oracle.com/javase/7/docs/api/java/lang/Math.html#floor(double)



Question 5. Conversion de types
-------------------------------

Comme d�crit dans la section |jn2.5.6|_ du livre de r�f�rence, il est possible en Java de r�aliser des conversions entre les nombres r�els et les nombres entiers. Certaines de ces conversions sont explicites, d'autres sont implicites. Consid�rons le fragment de code ci-dessous ::

 double f; 
 f=...; // ligne 1
 System.out.println(f);

Lorsqu'il est ex�cut�, il affiche la valeur ``2.0`` � l'�cran. Parmi les assignations ci-dessous, quelle est celle qui a plac� la valeur ``2.0`` dans la variable ``f`` ?

.. class:: positive

-
 ::

   f=125/(40+10);

 .. class:: comment

    Dans cette expression, le d�nominateur est une somme de nombres entiers, c'est donc lui-m�me un entier. Le num�rateur est un entier �galement. Donc, l'op�ration de division est une division *enti�re*. Le r�sultat de cette division enti�re est ``2`` qui est automatiquement converti par Java en la valeur r�elle ``2.0``.  Pour Java, cette assignation �quivaut en fait � ::

     f=(double) (125/(40+10));


.. class:: negative

-
 ::
   
   f=125/(40+10.0); 

 .. class:: comment

    Dans cette assignation, Java effectue une conversion de type implicite. Le d�nominateur devient automatiquement de type ``double`` et le calcul est une division de r�els.  Pour Java, cette assignation �quivaut en fait � ::

     f=((double) 125) / ((double) 40+10.0));
  
-
 ::

    f=125/(double) (40+10);

 .. class:: comment
  
    Dans cette assignation, le d�nominateur est obligatoirement un ``double``. La division est donc une division entre nombres r�els.

-
 ::

    f=125.0 / (40.0+10.0);

 .. class:: comment
  
    Dans cette assignation, le num�rateur et le d�nominateur sont de type ``double``. La division est donc une division entre nombres r�els.


Question 6. Cha�nes de caract�res
---------------------------------

Consid�rons le code Java ci-dessous qui d�clare et initialise des cha�nes de caract�res. ::

 String s1="abcdefghijklmnopqrstuvwxyz";

Laquelle des s�quences d'instructions ci-dessous affiche-t-elle ``OK`` � l'�cran ?

.. class:: positive

-
 ::

   char c=s1.charAt(5);
   if(c=='f') {
      System.out.println("OK");
   }

 .. class:: comment

    Voir http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#charAt(int) pour la documentation de la m�thode ``charAt``.

-
 ::

   char c=s1.charAt(0);
   if(c=='a') {
      System.out.println("OK");
   }

 .. class:: comment

    Voir http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#charAt(int) pour la documentation de la m�thode ``charAt``.


-
 ::

   char c=s1.charAt(s1.length()-1);
   if(c=='z') {
      System.out.println("OK");
   }

 .. class:: comment

    Voir http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#charAt(int) pour la documentation de la m�thode ``charAt``.


.. class:: negative


-
 ::

   char c=s1.charAt(4);
   if(c=='f') {
      System.out.println("OK");
   }

 .. class:: comment

    En Java, les caract�res d'un cha�ne de caract�res sont num�rot�s � partir de l'indice ``0``. L'indice ``4`` de la cha�ne de caract�res ``s1`` correspond donc au caract�re ``e``. Voir http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#charAt(int) pour la documentation de la m�thode ``charAt``.

-
 ::

   char c=s1.charAt(6);
   if(c=='f') {
      System.out.println("OK");
   }

 .. class:: comment

    En Java, les caract�res d'un cha�ne de caract�res sont num�rot�s � partir de l'indice ``0``. L'indice ``6`` de la cha�ne de caract�res ``s1`` correspond donc au caract�re ``g``. Voir http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#charAt(int) pour la documentation de la m�thode ``charAt``.

-
 ::

   char c=s1.charAt(1);
   if(c=='a') {
      System.out.println("OK");
   }

 .. class:: comment

    En Java, les caract�res d'un cha�ne de caract�res sont num�rot�s � partir de l'indice ``0``. L'indice ``1`` de la cha�ne de caract�res ``s1`` correspond donc au caract�re ``b``. Voir http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#charAt(int) pour la documentation de la m�thode ``charAt``.


-
 ::

   char c=s1.charAt(s1.length());
   if(c=='z') {
      System.out.println("OK");
   }

 .. class:: comment

    En Java, les caract�res d'un cha�ne de caract�res sont num�rot�s � partir de l'indice ``0``. ``s1.length()`` est le nombre de caract�res dans la cha�ne ``s1``.  Le dernier caract�re de cette cha�ne a donc l'indice ``s1.length()-1``. Il n'y a pas de caract�re � la position ``s1.length()``. Voir http://docs.oracle.com/javase/7/docs/api/java/lang/String.html#charAt(int) pour la documentation de la m�thode ``charAt``. 



Question 7. Extraction de cha�nes de caract�res
-----------------------------------------------

Dans la classe ``String``, la m�thode ``substring`` est une m�thode efficace pour extraire une sous-cha�ne d'une cha�ne de caract�res. En vous basant sur la description de ``substring`` dans le livre et dans la documentation Java http://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html, lequel des fragments de code ci-dessous affiche-t-il la cha�ne ``OK`` � l'�cran ?

.. class:: positive

-
 ::

   String s1="OOOO";
   String s2="KKKK";
   String s3=s1+s2;
   System.out.println(s3.substring(3,2));


-
 ::
 
   String s1="KOKOKO";
   String s3=s1+s1;
   System.out.println(s3.substring(5,2));
 
.. class:: negative

-
 ::

   String s1="OOOO";
   String s2="KKKK";
   String s3=s1+s2;
   System.out.println(s1.substring(4,2));

 .. class:: comment

    La cha�ne de caract�re ``s1`` ne contient que ``OOOO``. Il n'existe pas de caract�re � l'indice ``4`` dans cette cha�ne.

-
 ::

   String s1="OKOKO";
   String s2="OKOKO";
   String s3=s1+s2;
   System.out.println(s3.substring(4,2));

 .. class:: comment

    La cha�ne ``s3`` contient ``OKOKOOKOKO``. La cha�ne de caract�res extraite est donc ``OO``.




Question 8. M�thode ``indexOf``
-------------------------------

En Java, la m�thode ``indexOf`` peut �tre utilis�e pour d�terminer si une cha�ne de caract�res est comprise dans une autre cha�ne de caract�res. Consid�rons les d�clarations suivantes ::

 String s1="abcdef";
 String s2="mnopq";
 String s3="abcdefijklmnopqrstuvwxyz";

Laquelle des s�quences d'instructions ci-dessous affiche ``OK`` � l'�cran ?

.. class::  positive

-
 ::
 
   if(s3.indexOf(s2)>=0) {
      System.out.println("OK");
   }

-
 ::
 
   if(s3.indexOf(s1)>=0) {
      System.out.println("OK");
   }
 

.. class:: negative


-
 ::
 
   if(s1.indexOf(s2)>=0) {
      System.out.println("OK");
   }

 .. class:: comment

    Dans ce code, la m�thode ``indexOf`` est appliqu�e � la cha�ne de caract�res ``s1`` et prend comme argument la cha�ne de caract�res ``s2``. Elle d�termine donc si la cha�ne ``s2`` est une sous-cha�ne de ``s1``. Comme ce n'est pas le cas, elle retourne donc ``-1``.

-
 ::
 
   if(s2.indexOf(s3)>=0) {
      System.out.println("OK");
   }

 .. class:: comment

    Dans ce code, la m�thode ``indexOf`` est appliqu�e � la cha�ne de caract�res ``s2`` et prend comme argument la cha�ne de caract�res ``s3``. Elle d�termine donc si la cha�ne ``s3`` est une sous-cha�ne de ``s2``. Comme ce n'est pas le cas, elle retourne donc ``-1``.


-
 ::
 
   if(s2.indexOf(s3)>=0) {
      System.out.println("OK");
   }


 .. class:: comment

    Dans ce code, la m�thode ``indexOf`` est appliqu�e � la cha�ne de caract�res ``s2`` et prend comme argument la cha�ne de caract�res ``s3``. Elle d�termine donc si la cha�ne ``s3`` est une sous-cha�ne de ``s2``. Comme ce n'est pas le cas, elle retourne donc ``-1``.




Question 9. M�thodes de la classe ``String``
--------------------------------------------

La classe ``String`` contient de nombreuses m�thodes utiles de manipulation des cha�nes de caract�res. Certains retournent un bool�en, d'autres retournent un caract�re, d'autres encore retourne un ``String``. En consid�rant les d�clarations ci-dessous, quelle est la suite d'affirmations ci-dessous qui est vraie ? ::

 String s1="abcdef";
 String s2="mnopq";
 String s3="abcdefijklmnopqrstuvwxyz";

.. class:: positive

 - ``s1.equalsIgnoreCase(s2)`` est un bool�en, ``s1.charAt(2)`` est un caract�re et ``s3.indexOf(s2)`` est un entier

 - ``s1.equalsIgnoreCase(s2)`` est un bool�en, ``s2.length()`` est un entier et ``s1.substring(1,2)`` est une cha�ne de caract�res

.. class:: negative

 - ``s2.equalsIgnoreCase(s3)`` est un bool�en, ``s3.length()`` est un caract�re et ``s2.indexOf(s3)`` est un entier

 .. class:: comment

    La m�thode ``length`` retourne la longueur de la cha�ne de caract�re sur laquelle elle s'applique. Cette valeur est un entier.

 - ``s2.equalsIgnoreCase(s2)`` est un bool�en, ``s3.indexOf(s2)`` est un caract�re et ``s2.substring(1,2)`` une cha�ne de caract�res

 .. class:: comment

     La m�thode ``indexOf`` retourne un entier et non un caract�re.

 - ``s1.equalsIgnoreCase(s2)`` affiche ``true`` ou ``false``, ``s3.indexOf(s2)`` est entier et ``s2.substring(1,2)`` une cha�ne de caract�res

 .. class:: comment

    La m�thode ``equalsIgnoreCase`` retourne un bool�en, elle n'affiche rien.


Question 10. M�thode ``contains``
---------------------------------


Laquelle des impl�mentations de la m�thode ``contains`` dont la sp�cification et la signature sont reprises ci-dessous est-elle valide ? ::

 /*
  * @pre s non vide
  * @post retourne true si le caract�re c est pr�sent dans la cha�ne s et false sinon
  */

 public static boolean contains(String s, char c)

.. class:: positive

-
 ::

   {
    for(int i=0;i<s.length();i=i+1) {
      if(s.charAt(i)==c) {
         return true;
      }
    }
    return false;
   }


-
 ::

   {
    for(int j=s.length()-1;j>=0;j=j-1) {
      if(s.charAt(j)!=c) {
         return true;
      }
    }
    return false;
   }

.. class:: negative


-
 ::

   {
    for(int i=0;i<s.length();i=i+1) {
      if(s.charAt(i)!=c) {
         return false;
      }
    }
    return true;
   }

 .. class:: comment

    Cette m�thode retourne ``false`` d�s qu'un caract�re diff�re du caract�re pass� en argument, mais elle ne teste pas toute la cha�ne de caract�res. 

-
 ::

   {
    for(int j=s.length();j>=0;j=j-1) {
      if(s.charAt(j)==c) {
         return true;
      }
    }
    return false;
   }

 .. class:: comment

    Cette m�thode commence par essayer d'acc�der au caract�re � l'indice ``s.length()``, mais celui-ci n'existe pas puisque les indices des caract�res d'une cha�nes d�marrent � ``0``.


-
 ::

   {
    for(int j=s.length()-1;j>0;j=j-1) {
      if(s.charAt(j)==c) {
         return true;
      }
    }
    return false;
   }

 .. class:: comment

    Cette m�thode ne teste pas le caract�re se trouvant � l'indice ``0`` de la cha�ne de caract�res ``s``. Elle ne fonctionne donc pas dans tous les cas.
    
-
 ::

   {
    for(int i=0;i<=s.length();i=i+1) {
      if(s.charAt(i)==c) {
         return true;
      }
    }
    return false;
   }

 .. class:: comment

    Cette m�thode essaye de tester le caract�re � l'indice ``s.length()`` de la cha�ne de caract�res, mais ce caract�re n'existe pas. Cela provoquera une erreur � l'ex�cution.


-
 ::

   {
    for(int i=0;i<s.length();i=i+1) {
      if(s.charAt(i)==c) {
         return true;
      }
      else {
         return false;
      }
    }

   }

 .. class:: comment

    Cette m�thode teste uniquement la valeur du premier caract�re. Voyez-vous pourquoi ? 





.. include:: ../javanotes_toc.rst
