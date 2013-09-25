.. Copyright |copy| 2013 by Olivier Bonaventure
.. raw:: html

  <link href="css/prettify.css" type="text/css" rel="stylesheet" />
  <script type="text/javascript" src="js/jquery-1.7.2.min.js"></script>
  <script type="text/javascript" src="js/jquery-shuffle.js"></script>
  <script type="text/javascript" src="js/prettify.js"></script>
  <script type="text/javascript" src="js/rst-form.js"></script>
  <script type="text/javascript">$nmbr_prop = 4</script> 



====================================
Mission 3. M�thodes et sous-routines
====================================

Ces questions supposent que vous avez lu les sections suivantes du livre de r�f�rence |jn|_ 

 - |jn4|_
 
    - |jn4.1|_
    - |jn4.2|_
	
	- |jn4.2.1|_
	- |jn4.2.2|_
	- |jn4.2.3|_
	- |jn4.2.4|_
 
    - |jn4.3|_

        - |jn4.3.1|_
        - |jn4.3.2|_
        - |jn4.3.3|_
        - |jn4.3.4|_ 
        - |jn4.3.6|_
	 
    - |jn4.4|_

        - |jn4.4.1|_
        - |jn4.4.2|_
        - |jn4.4.3|_

    - |jn4.6|_

	- |jn4.6.1|_



Question 1. Appel de m�thodes de la classe ``Math``
---------------------------------------------------

La classe ``Math``, d�crite dans la section |jn2.3.1|_ du livre contient diff�rentes m�thodes de calcul. Celles-ci sont d�finies plus en d�tails dans http://docs.oracle.com/javase/6/docs/api/java/lang/Math.html. Parmi les fragments de programme ci-dessous, quels sont ceux qui sont corrects : 

.. class:: positive

-
 ::
 
    int i=1;
    int j=-1;
    double d=2.0;
    double e=3.0;
    int k=Math.abs(j);
    double f=Math.exp(d);
    double r=Math.rint(e);
    double w=Math.random();

-
 ::
 
    int i=1;
    int j=-1;
    double d=2.0;
    double e=3.0;
    int k=Math.abs(d);
    double f=Math.exp(e);
    double r=Math.rint(d);
    double x=Math.random();

.. class:: negative

-
 ::
 
    int i=1;
    int j=-1;
    double d=2.0;
    double e=3.0;
    int k=Math.abs(j);
    double f=Math.exp(e);
    int r=Math.rint(d);
    double w=Math.random();

 .. class:: comment

    La m�thode ``Math.rint`` prend comme argument un r�el et retourne un r�el (m�me si celui-ci a une valeur enti�re). Ceci vous est indiqu� par le type retourn� par la m�thode ``Math.rint`` dans la documentation.

-
 ::
 
    int i=1;
    int j=-1;
    double d=2.0;
    double e=3.0;
    int k=Math.abs(j);
    double f=Math.exp(i);
    double r=Math.rint(e);
    double w=Math.random();

 .. class:: comment

    La m�thode ``Math.exp`` prend comme argument un r�el. 



-
 ::
 
    int i=1;
    int j=-1;
    double d=2.0;
    double e=3.0;
    int k=Math.abs(j);
    double f=Math.exp(d);
    double r=Math.rint(e);
    int w=Math.random();

 .. class:: comment

    La m�thode ``Math.random`` retourne toujours une valeur de type ``double``.
    

-
 ::
 
    int i=1;
    int j=-1;
    double d=2.0;
    double e=3.0;
    int k=Math.abs(i);
    double h=Math.exp(e);
    double r=Math.rint(d);
    Math.random();

 .. class:: comment

    La m�thode ``Math.random`` retourne toujours une valeur de type ``double``. Elle ne peut donc jamais �tre utilis�e comme une m�thode ``void``.
    

Question 2. Utilisation de m�thodes
-----------------------------------

Un �tudiant �crit dans un programme Java le code suivant :

 ::

    double d=123.45;
    int i=12;
    if( f(d,i) ) { ... }

Quelle doit �tre la d�claration de la m�thode ``f`` pour que ce fragment de programme soit valide ?

.. class:: positive

- 
 ::

    public static boolean f( double d, int i) { 
     // code non fourni
    }

- 
 ::

    public static boolean f( double a, int b) {
     // code non fourni
    }


.. class:: negative

- 
 ::

    public static int f( int a, int b) { 
     // code non fourni
    }


 .. class:: comment

    Pour pouvoir �tre utilis�e dans une condition, la m�thode ``f`` doit retourner une valeur de type ``boolean``. La d�claration ci-dessus retourne une valeur de type ``int``. En outre, le premier argument de la m�thode ``f`` est un ``int`` alors que l'�tudiant passe un ``double``.

- 
 ::

    public static double f( double x, double y) { 
     // code non fourni
    }

 .. class:: comment

    Pour pouvoir �tre utilis�e dans une condition, la m�thode ``f`` doit retourner une valeur de type ``boolean``. La d�claration ci-dessus retourne une valeur de type ``double``. En outre, le second argument de la m�thode ``f`` est un ``double`` alors que l'�tudiant passe un ``int``.



   
Question 3. M�thodes permettant d'afficher
------------------------------------------

Un �tudiant souhaite une m�thode ``affiche`` permettant d'afficher ``n`` fois le caract�re ``X`` � l'�cran. La sp�cification de cette m�thode est ::

 /*
  * @pre n>0
  * @post affiche n fois le caract�re 'X' sur une ligne
  */


Il souhaite pouvoir utiliser cette m�thode de la fa�on suivante :

 ::

    int n=17;
    affiche(n);

Lors de son ex�cution, cette m�thode affiche � l'�cran ::

    XXXXXXXXXXXXXXXXX

Parmi les m�thodes d�finies ci-dessous, laquelle est une impl�mentation (signature et corps) correct de cette m�thode ``affiche`` ?


.. class:: positive

- 
 ::

    public static void affiche(int n) {
       for (int i=0;i<n;i=i+1) {
           System.out.print('X');
       }
       System.out.println();
    }

- 
 ::

    public static void affiche(int n) {
       for (int i=1;i<=n;i=i+1) {
           System.out.print('X');
       }
       System.out.println();
    }

- 
 ::

    public static void affiche(int n) {
       for (int i=n;i>0;i=i-1) {
           System.out.print('X');
       }
       System.out.println();
    }


.. class:: negative

- 
 ::

    public static int affiche(int nombre) {
       for (int j=0;j<nombre;j++) {
           System.out.print('X');
       }
       System.out.println();
    }

 .. class:: comment

    Cette m�thode ne se compile pas. Elle est d�clar�e comme retournant un ``int`` et ne contient pas d'instruction ``return``.
    
- 
 ::

    public static void affiche( nombre) {
       for (int j=0;j<nombre;j++) {
           System.out.print('X');
       }
       System.out.println();
    }

 .. class:: comment

    Cette m�thode ne se compile pas. Le type de son premier argument n'est pas sp�cifi�. 
    

- 
 ::

    public static void affiche(int n) {
       for (int i=1;i<=n;) {
           System.out.print('X');
       }
       System.out.println();
    }

 .. class:: comment

    Ce m�thode boucle ind�finiment. Pouvez-vous voir pourquoi ?

- 
 ::

    public static int affiche(int n) {
       for (int i=n;;i--) {
           System.out.print('X');
       }
       System.out.println();
    }

 .. class:: comment

    Cette m�thode boucle ind�finiment. Pouvez-vous voir pourquoi ?


Question 4. M�thodes ``void``
-----------------------------

En Java, les m�thodes de type ``void`` sont souvent utilis�es lorsqu'il faut ex�cuter une suite d'instructions qui ne doit pas retourner de valeur. On souhaite �crire une m�thode ``afficheSomme`` qui affiche � l'�cran la somme entre deux nombres entiers. Par exemple, en ex�cutant ``afficheSomme(3,4)``, la valeur ``7`` est affich�e � l'�cran. La sp�cification de cette m�thode est ::

 /*
  * @pre -
  * @post Affiche � l'�cran la somme des deux entiers pass�s en arguments
  */

.. class:: positive

- 
 ::
 
    public static void afficheSomme(int a, int b) 
    {
       int somme=a+b;
       System.out.println(somme);
    }

- 
 ::
 
    public static void afficheSomme(int x, int y) 
    {
       System.out.println(x+y);
    }
 
 .. class:: comment

     L'expression ``x+y`` est une expression qui a comme valeur un entier. Elle peut donc bien �tre utilis�e comme argument de la m�thode ``System.out.println()``.

.. class:: negative

- 
 ::
 
    public static void afficheSomme(a, b) 
    {
       int s=a+b;
       System.out.println(s);
    }

 .. class:: comment

    Lors de la d�claration d'une m�thode, il est n�cessaire de sp�cifier le type de chacun de ses arguments. Cette d�claration n'est pas valide.
-
 ::
 
    public static void afficheSomme(int c, int d) 
    {
       int sum=c+d;
    }

 .. class:: comment

    Cette m�thode calcule la somme de ses deux arguments mais ne l'affiche pas � l'�cran comme demand�.

- 
 ::
 
    public static void afficheSomme(double c, double d) 
    {
       System.out.println(x+y);
    }

 .. class:: comment

    Cette m�thode prend comme arguments deux nombres r�els et non deux entiers comme demand� dans l'�nonc�.


Question 5. D�clarations de m�thodes
------------------------------------

En Java, la d�claration d'une m�thode nous renseigne sur le type de valeur qui est retourn� par cette m�thode. Consid�rons les d�finitions de m�thodes ci-dessous.

::

   public static void v(int i)  {
     // code non fourni
   }
   public static void w()  {
     // code non fourni
   }
   public static int f(int i)  {
     // code non fourni
   }
   public static int g(boolean b)  {
     // code non fourni
   }
   public static int h()  {
     // code non fourni
   }

Une seule des s�quences d'instructions ci-dessous est valide. Pourriez-vous indiquer laquelle ?


.. class:: positive

-
 ::

    int a=f(2);
    int b=g(false);
    int c=h();
    w();
    
- 
 ::

    int a=g(true); 
    int b=f(-2);
    int c=h();
    v(a);

- 
 ::

    int a=g(false); 
    int b=f(a-2);
    int c=h();
    v(a);


 .. class:: comment

    Ce fragment de code est valide. Notez que l'argument de la m�thode ``f`` peut �tre n'importe quelle expression qui retourne une valeur de type ``int``. C'est bien le cas pour l'expression ``a-2`` puisque la variable ``a`` est de type ``int``.

-
 ::

    int b=f(-2);
    int a=g(b==1); 
    int c=h();
    v(a);

 .. class:: comment

    Ce fragment de code est valide. Notez que l'argument de la m�thode ``g`` peut �tre n'importe quelle expression qui retourne une valeur de type ``boolean``. C'est bien le cas pour l'expression ``b==1``.

.. class:: negative 

-
 ::

    int a=g(false); 
    int b=f(-2);
    int c=w();
    h();
    
 .. class:: comment

    Ce fragment de code contient deux erreurs. Relisez la d�finition des m�thodes ``h`` et ``w``. La premi�re (``h``) retourne une valeur enti�re. Elle ne peut donc �tre utilis�e que dans une expression qui donne un r�sultat entier.  La seconde (``w``) est de type ``void``, elle ne retourne donc aucune valeur et ne peut pas �tre utilis�e comme membre de droite d'une instruction d'affectation.
  
-
 ::

    int a=g(false); 
    int b=f(-2.0);
    int d=h();
    v(d); 

 .. class:: comment

    Quel est le type de la valeur ``2.0`` en Java ? La m�thode ``f`` prend un argument de type `�nt``.


- 
 ::

    int a=g(1); 
    int b=f(7);
    int c=h();
    w(); 


Question 6. M�thodes retournant un nombre
-----------------------------------------


La classe ``Math`` de java contient la m�thode ``Math.min``. Celle-ci prend deux arguments de type ``double`` et retourne le plus petit des deux nombres pass�s en argument. 
Laquelle de ces m�thodes reprises ci-dessous est-elle une impl�mentation correcte de cette m�thode ``min`` dont la sp�cification est ::

 /*
  * @pre -
  * @post retourne le minimum entre les deux arguments
  */

.. class:: positive

- 
 ::

    public static double min (double a, double b) {
      if (a<b) {
          return a;
      }
      return b;
    }

  .. class:: comment

     Cette impl�mentation est correct. Lorsque ``a<b``, la m�thode se termine par ``return a;``. L'instruction ``return b;`` n'est ex�cut�e que si ``b>=a``.
    

- 
 ::

    public static double min (double a, double b) {
      if (a<b) {
          return a;
      } 
      else {
          return b;
      }
    }

- 
 ::

    public static double min (double a, double b) {
      if (b<a) {
          return b;
      } 
      else {
          return a;
      }
    }

.. class:: negative

-
 ::

    public static double min (double a, double b) {
      if (b<a) {
          System.out.println(b);
      } 
      else {
          System.out.println(a);
      }
    }

 .. class:: comment

    Ne confondez pas une m�thode qui "affiche" (en utilisant ``System.out.println``) avec une m�thode qui retourne une valeur. Un m�thode qui retourne une valeur doit toujours se termine par ``return``. ``javac`` n'acceptera pas de compiler cette m�thode qui ne retourne pas de valeur.

-
 ::

    public static double min (double a, double b) {
      if (b<a) {
          return b;
      } 
    }
  
 .. class:: comment

    Cette m�thode ne se compile pas. En Java, une m�thode ``double`` doit toujours retourner, via l'instruction ``return``, une valeur de type ``double``, quel que soit l'ex�cution de cette m�thode. Cette version ne retourne de valeur que lorsque ``b<a``. 

-
 ::

    public static void min (double a, double b) {
      if (b<a) {
          return b;
      } 
      return a;
    }
    
 .. class:: comment

    Une m�thode ``void`` ne retourne aucun r�sultat. Ce code ne correspond pas � ce qui est demand�.


Question 7. M�thodes retournant un bool�en
------------------------------------------


Lorsque l'on doit manipuler des conditions complexes dans une instruction conditionnelle ou une boucle, il peut �tre int�ressant d'�crire des m�thodes qui retournent un bool�en. Sachant que l'expression ``a%b`` retourne le reste de la division euclidienne de la valeur de la variable enti�re ``a`` par ``b``, laquelle des m�thodes ci-dessous est-elle une impl�mentation de la sp�cification suivante ::

 /*
  * @pre n>0
  * @post retourne true lorsque le nombre pass� en argument est pair et false dans le cas contraire
  */

.. class:: positive

-
 ::

    public static boolean pair(int n) {
      int reste=n%2;
      return (reste==0);
    }     

-
 ::

    public static boolean pair(int n) {
      int reste=n%2;
      boolean pair=(reste==0);
      return pair;
    }     

-
 ::

    public static boolean pair(int n) {
      int reste=n%2;
      if (reste!=0) {
          return false;
      }
      else {
          return true;
      }
    }

 .. class:: comment

    Ce code est correct, mais il est inutilement long. Sachant que l'instruction conditionnelle �value une condition qui a d�j� une valeur bool�enne, il est pr�f�rable de retourner directement une telle expression. Comme dans le code ci-dessous ::

       public static boolean pair(int n) {
        int reste=n%2;
        return (reste==0);
       }    


.. class:: negative

-
 ::

    public static boolean pair(int n) {
      int reste=n%2;
      return (reste!=0);
    }     

 .. class:: comment

    Cette m�thode retourne ``true`` lorsque x est impair et ``false`` sinon.

-
 ::

    public static boolean pair(double n) {
      int reste=n%2;
      return (reste=0);
    }     

 .. class:: comment

    L'argument de la m�thode doit n�cessairement �tre de type ``int`` pour pouvoir utiliser le reste de la division euclidienne. En outre, ``reste=0`` est une affectation et non une expression bool�enne que l'on peut passer comme argument � ``return``.

-
 ::

    public static boolean pair(int n) {
      int reste=n%2;
      return reste;
    }     

 .. class:: comment

    Ce fragment de code est incorrect. La d�finition de la m�thode sp�cifie qu'elle retourne une valeur bool�enne. Or, ``reste`` est une variable de type ``int``. 


-
 ::

    public static boolean pair(int n) {
      int reste=n%2;
      if (reste!=0) {
          return false;
      }
    }

 .. class:: comment

    Cette m�thode ne se compile pas. Elle ne d�finit pas correctement la valeur qu'il faut retourner lorsque ``reste==0``. 


Question 8. Calcul du maximum
-----------------------------

La classe ``Math`` contient de nombreuses m�thodes. Vous trouverez notamment la m�thode ``Math.max(double a, double b)`` qui calcule le maximum entre les deux nombres pass�s en argument. Laquelle des m�thodes ci-dessous est-elle une impl�mentation de la sp�cification suivante ::

 /*
  * @pre -
  * @post retourne le maxium entre les deux r�els pass�s en arguments
  */



.. class:: positive

-
 ::

    public static double max(double a, double b)
    {
      if(a>b) {
         return a;
      }
      else
      {
         return b;
      }
    }

- 
 ::

    public static double max(double a, double b)
    {
      if(a<=b) {
         return b;
      }
      else
      {
         return a;
      }
    }

- 
 ::

    public static double max(double a, double b)
    {
      if(a<=b) {
         return b;
      }
      return a;
    }

 .. class:: comment

    Ce code est correct. Il est cependant un peu moins lisible qu'un programme dans lequel ``return a;`` se trouverait � l'int�rieur d'un bloc ``else``.

 
    
.. class:: negative

-
 ::

    public static double max(double a, double b)
    {
      if(a>b) {
         return a;
      }
      else
      {
         return a;
      }
    }

 .. class:: comment

    Ce code retourne toujours la m�me valeur.

-
 ::

    public static double max(double a, double b)
    {
         return a;
    }

 .. class:: comment

    Ce code retourne toujours la m�me valeur.


- 
 ::

    public static double max(double a, double b)
    {
      if(a>=b) {
         return a;
      }
    }

 .. class:: comment

    Ce code ne compile pas. La m�thode ``max`` propos�e ne retourne pas de valeur lorsque ``a<b``.

- 
 ::

    public static double max(double a, double b)
    {
      if(a>=b) {
         return b;
      }
      return a;
    }

 .. class:: comment

    Ce code retourne en fait le ``minimum`` entre les nombres ``a`` et ``b`` pass�s en arguments.


Question 9. Calcul de la valeur absolue
---------------------------------------


Dans le programme Java suivant, un �tudiant souhaite utiliser une m�thode ``abs`` permettant de calculer la valeur absolue d'un nombre.

 ::
     
    int i=1401;
    double d=-112.4;
    double j=d+abs(2*d);


.. class:: positive

-
 ::

    public static double abs(double c) {
       double r=c;
       if(c<0) {
         r=-c;
       }
       return r;
    }

-
 ::

    public static double abs(double c) {
       if(c>=0) {
         return c;
       }
       return (-c);
    }

	 
.. class:: negative

-
 ::

    public static int abs(double c) {
       if(c<0) {
         return (-c);
       }
       return c;
    }

 .. class:: comment

    Le code utilis� par l'�tudiant s'attend � recevoir un ``double``. La m�thode doit �galement retourner un ``double`` et non un ``int`` comme ci-dessus.
-
 ::

    public static double abs(int a) {
       if(a>0) {
         return a;
       }
       return (-a);
    }

 .. class:: comment

    La m�thode propos�e prend comme argument un entier alors que l'�tudiant fournit un r�el.	 

-
 ::

    public static double abs(double c) {
       double r;
       if(c<0) {
         r=-c;
       }
       return r;
    }

 .. class:: comment

    Cette m�thode ne compile pas. La variable ``r`` peut �tre utilis�e sans avoir �t� initialis�e. C'est le cas par exemple lorsque ``c>0``. Le compilateur Java refusera de compiler cette m�thode.

-
 ::

    public static double abs(double c) {
       if(c>=0) {
         return;
       }
       return (-c);
    }

 .. class:: comment

    Cette m�thode ne compile pas. La premi�re invocation de ``return`` ne retourne par de valeur tandis que la seconde retourne un r�el.


Question 10. Les nombres amicaux
--------------------------------


Deux nombres entiers positifs sont dits `amicaux <http://fr.wikipedia.org/wiki/Nombre_amical>`_ si la somme des diviseurs entiers de l'un est �gal � la somme des diviseurs entiers de l'autre. Pour v�rifier si deux nombres sont amicaux, le plus simple est d'utiliser une m�thode qui calcule la somme des diviseurs entiers d'un nombre et d'ensuite comparer les deux sommes. Supposons que cette m�thode existe et est d�finie comme suit :

 ::

    /*
     * @pre : n>0
     * @post : retourne la somme des diviseurs entiers de n
     */
    public static int sdiv(int n) {
      // code non fourni
    }

Laquelle des m�thodes ci-dessous retourne-t-elle ``true`` lorsque les deux nombres pass�s en argument sont amicaux et ``false``  sinon ?

.. class:: positive

-
 ::

    public static boolean amical(int a, int b) {
       int sdiv1=sdiv(a);
       int sdiv2=sdiv(b);
       return (sdiv1==sdiv2);
    }

-
 ::

    public static boolean amical(int a, int b) {
       return (sdiv(a)==sdiv(b));
    }

.. class:: negative

- 
 ::

    public static int amical(int a, int b) {
       int sdiv1=sdiv(a);
       int sdiv2=sdiv(b);
       return (sdiv1==sdiv2);
    }

 .. class:: comment
 
    Cette m�thode est d�finie comme retournant un entier alors qu'elle retourne en fait un bool�en. Elle ne se compile pas.


- 
 ::

    public static boolean amical(int a, int b) {
       int sdiv1=sdiv(a);
       int sdiv2=sdiv(b);
    }

 .. class:: comment
 
    Cette m�thode est d�finie comme retournant un bool�en alors qu'elle retourne rien. Elle ne se compile pas.


- 
 ::

    public static boolean amical(int c, int d) {
       sdiv1=sdiv(d);
       sdiv2=sdiv(c);
       return (sdiv1==sdiv2);
    }

 .. class:: comment
 
    Cette m�thode ne se compile pas. Les variables ``sdiv1`` et ``sdiv2`` doivent �tre d�clar�es avant de pouvoir �tre utilis�es.






.. include:: ../javanotes_toc.rst
