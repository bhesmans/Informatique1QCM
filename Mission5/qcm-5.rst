.. Copyright |copy| 2013 by Olivier Bonaventure
.. raw:: html

  <link href="css/prettify.css" type="text/css" rel="stylesheet" />
  <script type="text/javascript" src="js/jquery-1.7.2.min.js"></script>
  <script type="text/javascript" src="js/jquery-shuffle.js"></script>
  <script type="text/javascript" src="js/prettify.js"></script>
  <script type="text/javascript" src="js/rst-form.js"></script>
  <script type="text/javascript">$nmbr_prop = 4</script> 



===================
Mission 5. Tableaux
===================


Ces questions supposent que vous avez lu les sections suivantes du livre de r�f�rence |jn|_ 

 - |jn2|_
 
  - |jn2.5|_

    - |jn2.5.7|_

 - |jn7|_

  - |jn7.1|_

    - |jn7.1.1|_
    - |jn7.1.2|_
    - |jn7.1.3|_ 

  - |jn7.2|_

    - |jn7.2.1|_
    - |jn7.2.3|_
    - |jn7.2.4|_ 
    - |jn7.2.6|_ 
  
  - |jn7.4|_

    - |jn7.4.1|_

  - |jn7.5|_

    - |jn7.5.1|_
    - |jn7.5.2|_
   
 - |jn8|_

  - |jn8.4|_

    - |jn8.4.1|_


Les sections vues pr�c�demment restent bien entendu d'actualit�.


Question 1. D�claration de tableaux
-----------------------------------

Parmi les d�clarations suivantes, quelle est celle qui permet de d�clarer correctement un tableau dont la r�f�rence est d�nomm�e ``tab`` et qui peut contenir 5 nombres entiers ?


.. class:: positive

- ::

    int[] tab=new int[5];

  .. class:: comment

     C'est la d�claration la plus courante pour un tableau d'entiers. Notez que cette ligne combine une d�claration (``int[] tab`` et la cr�ation du tableau correspondant permettant de stocker 5 �l�ments de type ``int``.

- ::
    
    int[] tab;
    tab=new int[5];

  .. class:: comment

     La premi�re ligne d�clare que ``tab`` est une r�f�rence vers un tableau d'entiers. La deuxi�me ligne associe cette r�f�rence � un tableau permettant de stocker 5 entiers.


.. class:: negative

- ::
  
     tab=int [5];

  .. class:: comment

     Cette ligne est incorrecte. ``tab`` n'a pas �t� d�clar� pr�alablement et il faut utiliser le mot cl� ``new`` pour initialiser un tableau. Relisez |jn7.1.3|_ 

- ::

     tab=new int[5];

  .. class:: comment

     Cette ligne est incorrecte. ``tab`` n'a pas �t� d�clar� pr�alablement. Il faut faire pr�c�der cette ligne d'une d�claration de ``tab``. Relisez |jn7.1.3|_ 

- ::


     int[] tab=new int[];

  .. class:: comment

     Cette ligne est incorrecte. Lorsque l'on initialise un tableau, il faut sp�cifier le nombre d'�l�ments du tableau entre [] dans le membre de droite. En Java, les tableaux ont une taille fixe qui est d�finie � leur cr�ation. Relisez |jn7.1.3|_ 

- ::
  
     int[5] tab=new int[];

  .. class:: comment

     Cette ligne est incorrecte. Lorsque l'on initialise un tableau, il faut sp�cifier le nombre d'�l�ments du tableau entre [] dans le membre de droite. En Java, les tableaux ont une taille fixe qui est d�finie � leur cr�ation. Relisez |jn7.1.3|_ 

- ::

     int tab[5]=new int[];

  .. class:: comment

     Cette ligne est incorrecte. Lorsque l'on initialise un tableau, il faut sp�cifier le nombre d'�l�ments du tableau entre [] dans le membre de droite. Relisez |jn7.1.3|_ 

     

Question 2. Initialisation de tableaux
--------------------------------------

Laquelle des lignes ci-dessous d�clare un tableau contenant trois nombres r�els et l'initialise avec les valeurs ``-1.0``, ``0.0`` et ``1.0``.


.. class:: positive

- ::

     double[] t=new double[] { -1.0, 0.0, 1.0};
 
  .. class:: comment

     Cette ligne est correcte. Le livre la pr�f�re � la ligne ``double[] t= { -1.0, 0.0, 1.0};`` m�me si les deux sont �quivalentes pour Java.

- ::

     double[] t= { -1.0, 0.0, 1.0};

  .. class:: comment

     Cette ligne est correcte. Le livre pr�f�re la ligne ``double[] t=new double[] { -1.0, 0.0, 1.0};`` qui est plus explicite m�me si les deux sont �quivalentes pour Java.


.. class:: negative

- ::

    double[3] t= {-1.0, 0.0, 1.0};

  .. class:: comment

    En Java, il n'existe pas de type ``double[3]`` pouvant �tre mis dans une d�claration. Relisez |jn7.1.3|_ 

- ::

    double t= {-1.0, 0.0, 1.0};

  .. class:: comment

    En Java, ``double t`` d�clare un r�el et non un tableau de r�els. Relisez |jn7.1.3|_ 


- ::

    double[] t= new double[-1.0, 0.0,1.0];


  .. class:: comment

     Cette ligne n'est pas syntaxiquement correcte, relisez |jn7.1.3|_ 

- ::

    double[] t= new double{-1.0,0.0,1.0};

  .. class:: comment

     Cette ligne n'est pas syntaxiquement correcte, relisez |jn7.1.3|_ 


- ::

    double[] t= [-1.0, 0.0, 1.0];

  .. class:: comment

     Cette ligne n'est pas syntaxiquement correcte. Ne confondez pas ``{`` et ``[``. Relisez |jn7.1.3|_ 



Question 3. Initialisation de tableaux
--------------------------------------

Une fois qu'un tableau a �t� d�clar� et initialis�, il faut parfois pouvoir conna�tre le nombre d'�l�ments se trouvant dans le tableau. Lequel des codes ci-dessous affiche-t-il le nombre d'entiers dans le tableau ``tab`` d�clar� via ``int[] tab=new int[]{1,2,7,9,3,99,-12,78,119}`` ?

.. class:: positive

- ::

    System.out.println(tab.length);

.. class:: negative

- ::

    System.out.println(tab.length());

  .. class:: comment

     En Java, la syntaxe ``tab.length()`` correspond � l'ex�cution de la m�thode ``length()`` sur l'objet dont la r�f�rence est ``tab``. Les tableaux Java ne sont pas des objets ayant des m�thodes que l'on peut appeler. Relisez |jn7.1.2|_


- ::

    System.out.println(tab.size);

  .. class:: comment

     ``tab.size`` n'existe pas. Relisez |jn7.1.2|_  

- ::

    System.out.println(tab[0]);

  .. class:: comment

     ``tab[0]`` est le premier �l�ment du tableau ``tab`` et non le nombre d'�l�ments pr�sents dans le tableau. Relisez |jn7.1.2|_  

- ::

    System.out.println(tab.[length]);

 .. class:: comment

     Cette ligne est syntaxiquement incorrecte. Relisez |jn7.1.2|_  

Question 4. Tableaux � plusieurs dimensions
-------------------------------------------

Outre les tableaux � une dimension d�crit dans |jn7.1|_, Java supporte �galement des tableaux � plusieurs dimensions. Laquelle des d�clarations ci-dessous est-elle un tableau � plusieurs dimensions qui permet de stocker exactement 24 nombres entiers ?

.. class:: positive

- ::

    int[][] t=new int[4][6];
   
  .. class:: comment

     Ce tableau � deux dimensions comprend 4 lignes et 6 colonnes.
 

- ::

    int[][] t=new int[3][8];

  .. class:: comment

     Ce tableau � deux dimensions comprend 3 lignes et 8 colonnes.

.. class:: negative

- ::

    int[][] t=new int[2][4];

  .. class:: comment

     Ce tableau � deux dimensions comprend 2 lignes et 4 colonnes. Relisez |jn7.5.1|_


- ::

    int[][] t=new int[24];

  .. class:: comment

     Cette ligne est erron�e. La r�f�rence d�clar�e � gauche est vers un tableau de tableaux alors que seul un tableau d'entiers est cr�� dans le membre de droite. Relisez |jn7.5.1|_

- ::

    int[] t=new int[3][8];

  .. class:: comment

     Cette ligne est erron�e. La r�f�rence d�clar�e � gauche est vers un tableau alors qu'un tableau de tableaux d'entiers est cr�� dans le membre de droite. Relisez |jn7.5.1|_


- ::

    int[][] t=new int[2][4];

  .. class:: comment

     Le tableau cr�� a deux lignes et 4 colonnes. Il ne permet donc pas de stocker 24 nombres entiers. Relisez |jn7.5.1|_



Question 5. Tableaux ordonn�s
-----------------------------

Laquelle des suites d'instructions ci-dessous est une impl�mentation correcte de la sp�cification suivante : ::

 /**
  * @pre  t est un tableau contenant au moins un �l�ment 
  * @post retourne true si les donn�es du tableau t sont en ordre 
  *       d�croissant, false sinon
  */
  public static boolean decroissant(double[] t)
  {
    // corps � inclure
  }


.. class:: positive

- ::

    if(t.length==1) {
        return true;
    }
    for(int i=1;i<t.length;i++) {
      if (t[i-1] <= t[i]) {
            return false; 
      }
    }
    return true; 


- ::

    if(t.length==1) {
        return true;
    }
    for(int i=t.length-1;i>=1;i=i-1) {
      if (t[i-1] <= t[i]) {
            return false; 
      }
    }
    return true; 

.. class:: negative 


- ::

    if(t.length==1) {
        return true;
    }
    for(int i=0;i<t.length;i++) {
      if (t[i-1] <= t[i]) {
            return false; 
      }
    }
    return true; 

  .. class:: comment

     Que se passe-t-il lors du premier passage dans la boucle ``for`` avec un tableau ``t`` contenant ``{ 1.0, 2.0 }`` ? ``i`` vaut ``0``, quel est la valeur de ``t[0-1]`` ?

- ::

    if(t.length==1) {
        return true;
    }
    for(int i=t.length;i>=1;i=i-1) {
      if (t[i-1] <= t[i]) {
            return false; 
      }
    }
    return true; 

  .. class:: comment

     Que se passe-t-il lors du premier passage dans la boucle ``for`` avec un tableau ``t`` contenant ``{ 1.0, 2.0 }`` ? ``i`` vaut ``t.length``, quel est la valeur de ``t[i]`` ?

- ::

    if(t.length==1) {
        return true;
    }
    for(int i=1;i<t.length;i++) {
      if (t[i-1] <= t[i]) {
         return false; 
      }
      else  {
        return true;
      }
    }
    return true; 

  .. class:: comment

     Cette m�thode teste-t-elle vraiment l'enti�ret� du tableau ? Combien de fois passe-t-elle dans la boucle ``for`` ?


- ::

    if(t.length==1) {
        return true;
    }
    for(int i=t.length-1;i>=1;i=i-1) {
      if (t[i-1] <= t[i]) {
         return false; 
      }
      else {
         return true; 
      }	  
    }
    return true; 

  .. class:: comment

     Cette m�thode teste-t-elle vraiment l'enti�ret� du tableau ? Combien de fois passe-t-elle dans la boucle ``for`` ?

Question 6. Initialisation de tableaux � deux dimensions
--------------------------------------------------------

Consid�rons un tableau � deux dimensions initialis� comme suit : ::

 int[][] tab= {  { 1,2,3} ,
                 { 4,5} 
	      } ;

Laquelle des expressions bool�ennes ci-dessous est-elle vraie ?

.. class:: positive

- ::

     (tab[0].length==3) && (tab[1][1]==5)


- ::

     (tab.length==2) && (tab[0][2]==3)


.. class:: negative

- ::

    (tab.length==1) && (tab[1][1]==4)

  .. class:: comment

     ``tab.length`` est le nombre de lignes du tableau ``tab``, c'est-�-dire ``2``.  Relisez |jn7.5.1|_ et |jn7.5.2|_

- ::

    (tab[1].length==3) && (tab[0][1]==2)

  .. class:: comment

     ``tab[1].length`` est le nombre de colonnes de la ligne ``1`` du tableau, c'est-�-dire ``2``.  Relisez |jn7.5.1|_ et |jn7.5.2|_


- ::

    (tab[0][2]==2) && (tab[1][0]==4)

 
  .. class:: comment

     L'�l�ment ``tab[0][2]`` a comme valeur ``3`` et non ``2``.


Question 7. Manipulation de tableau � deux dimensions 
-----------------------------------------------------

Consid�rons la matrice ``m`` de ``li`` lignes et ``c`` colonnes qui a �t� initialis�e par les instructions ci-dessous : ::


   double m[][]=new double[li][c];
   int count=1;
   for(int i=0;i<li;i++) {
     for(int j=0; j<c; j++) {
         m[i][j]=count;
	 count++;
     }
   }

Laquelle des expressions bool�ennes ci-dessous est-elle vraie ?


.. class:: positive

- ::

     ( m[li-1][0]==((li-1)*c)+1) && (m[0][c-1]==c)

- ::

     ( m[0][0]==1) && (m[li-1][c-1]==1+li*ci)


.. class:: negative

- ::

     ( m[0][c-1]==c-1)

  .. class:: comment

     Cet �l�ment de la matrice vaut ``c`` et car ``count`` est incr�ment�e � chaque passage dans la boucle ``for j<c``.

    
- ::

     ( m[li][c]==li*ci)
     

  .. class:: comment

     Il n'existe pas d'�l�ment ``m[li][c]`` dans la matrice ``m``.

- ::

     (m[0][0]==0) && (m[0][c-1]==c)

  .. class:: comment

     ``count`` �tant initialis� � ``1``, l'�l�ment ``m[0][0]`` est initialis� � la valeur ``1``.

- ::

      ( m[0][1]==1) && (m[0][c-1]==c)


  .. class:: comment

     ``m[0][1]`` vaut ``2``



Question 8. Somme des �l�ments d'un tableau
-------------------------------------------

Laquelle des impl�mentations suivantes est-elle une impl�mentation correcte de la m�thode ``sumTab`` dont la sp�cification est reprise ci-dessous : ::


  /*
   * @pre tableau contenant au moins un �l�ment
   * @post retourne la somme des valeurs stock�es dans le tableau
   */
  public static double sumTab(double[] t)


.. class:: positive


- ::

   double sum=0.0;
   for(int i=0;i<t.length;i++) {
     sum=sum+t[i];
   }
   return sum;


- ::

   double sum=0.0;
   for(int i=t.length-1;i>=0;i=i-1) {
     sum=sum+t[i];
   }
   return sum;

.. class:: negative

- ::

   double sum=0.0;
   for(int i=0;i<t.length;i++) {
    for(int j=0;j<t[i].length;j++) {
     sum=sum+t[i];
    }
   }
   return sum;

  .. class:: comment

     Ce code est utilisable pour calculer la somme des �l�ments d'un tableau � deux dimensions, mais le tableau ``t`` qui est pass� comme param�tre effectif � la m�thode est un tableau � une seule dimension. Ce code ne compilera pas dans la m�thode ``sumTab``.

- ::

   double sum=0.0;
   for(int i=t.length-1;i>=0;i=i-1) {
    for(int j=0;j<t[i].length;j++) {
     sum=sum+t[i];
    }
   }
   return sum;

  .. class:: comment

     Ce code est utilisable pour calculer la somme des �l�ments d'un tableau � deux dimensions, mais le tableau ``t`` qui est pass� comme param�tre effectif � la m�thode est un tableau � une seule dimension. Ce code ne compilera pas dans la m�thode ``sumTab``.


- ::

    double sum=0.0;
    for(int i=0;i<=t.length;i++) {
      sum=sum+t[i];
    }
    return sum;
 
  .. class:: comment

     Ce code provoquera une erreur � l'ex�cution. Il n'y a pas d'�l�ment dans le tableau ``t`` � l'indice ``t.length``. L'indice le plus �lev� du tableau est ``t.length-1``.

Question 9. Assertions
----------------------

En Java, les assertions peuvent �tre utilis�es pour v�rifier explicitement les pr�conditions et les postconditions d'une m�thode. En programmation d�fensive, on utilise des ``assert`` pour v�rifier explicitement les pr�conditions de chaque m�thode. Consid�rons la m�thode dont la sp�cification est reprise ci-dessous : ::
 
 /**
  * @pre a>0, b>2*a et b est pair
  * @post ....
  */
 private void methode(int a, int b)

Laquelle des s�quences d'instructions ci-dessous v�rifie explicitement les pr�conditions de cette m�thode ?

.. class:: positive

- ::

    assert a>0 : "a doit �tre strictement positif";
    assert ( (b>2*a) && (b%2)==0 ) : "b invalide";

  .. class:: comment

     Notez qu'en Java l'expression ``(b%2)`` est une expression enti�re. Elle peut donc appara�tre � gauche d'un signe ``==``. Il est int�ressant d'utiliser des commentaires pour indiquer quelle pr�condition n'est pas v�rifi�e.
 
- ::

    assert a>0 : "a doit �tre strictement positif";
    assert (b>2*a) : "b trop petit";
    int reste=b%2;
    assert reste==0 : "b n'est pas pair";  

  .. class:: comment

     Il est int�ressant d'utiliser des commentaires pour indiquer quelle pr�condition n'est pas v�rifi�e.  

.. class:: negative

- ::

    assert a<=0; 
    assert ( (b>2*a) && (b%2)==0 ) : "b invalide";

  .. class:: comment

     La premi�re assertion est incorrecte. Elle est vraie lorsque ``a<=0`` or la pr�condition de la m�thode est ``a>0``.

- ::

    int reste=b%2;
    assert a<=0 : "a doit �tre strictement positif";
    assert reste!=0 : "b n'est pas pair";    
    assert (b<=2*a) : "b trop petit";

  .. class:: comment

     En Java, ``assert`` permet de v�rifier qu'une pr�condition est remplie. Si c'est le cas, l'instruction ``assert`` n'a aucun effet. Sinon, l'instruction ``assert`` affiche le message qui suit ``:`` et provoque une erreur. Lorsque l'on utilise ``assert`` pour v�rifier les pr�conditions, on souhaite que l'ex�cution du programme s'arr�te et que le message d'erreur soit afficher lorsqu'une pr�condition n'est pas v�rifi�e. Pour cela, l'expression bool�enne contenu dans l'assertion doit �tre la pr�condition � v�rifier.

- ::

    assert a<=0 : "a doit �tre strictement positif";
    assert ( (b<=2*a) && (b%2)!=0 ) : "b invalide";

  .. class:: comment

     Notez qu'en Java l'expression ``(b%2)`` est une expression enti�re. Elle peut donc appara�tre � gauche d'un signe ``==``. En Java, ``assert`` permet de v�rifier qu'une pr�condition est remplie. Si c'est le cas, l'instruction ``assert`` n'a aucun effet. Sinon, l'instruction ``assert`` affiche le message qui suit ``:`` et provoque une erreur. Lorsque l'on utilise ``assert`` pour v�rifier les pr�conditions, on souhaite que l'ex�cution du programme s'arr�te et que le message d'erreur soit afficher lorsqu'une pr�condition n'est pas v�rifi�e. Pour cela, l'expression bool�enne contenu dans l'assertion doit �tre la pr�condition � v�rifier.


Question 10. Somme de vecteurs
------------------------------

Consid�rons les tableaux ``a``, ``b`` et ``s`` d�clar�s comme indiqu�s ci-dessous : ::

  int[] a=new int[20];
  int[] b=new int[20];
  int[] s=new int[20];


Supposons que ces tableaux servent � stocker des vecteurs (au sens math�matique du terme). Laquelle des s�quences d'instructions ci-dessous place-t-elle dans le vecteur ``s`` la somme des vecteurs ``a`` et ``b``? 

.. class:: positive

- ::

     for(int i=0; i<a.length;i++) {
      s[i]=a[i]+b[i]; 
     }

- ::

     for(int i=0; i<b.length;i++) {
      s[i]=a[i]+b[i]; 
     }

- ::

     for(int i=s.length-1; i>=0;i=i-1) {
      s[i]=a[i]+b[i]; 
     }

.. class:: negative

- ::

     s[]=a[]+b[];

  .. class:: comment

     Cette instruction est invalide en Java. Il est n�cessaire d'utiliser une boucle pour calculer cette somme.

- ::

     for(int i=0; i<=a.length;i++) {
      s[i]=a[i]+b[i]; 
     }

  .. class:: comment

     Cette boucle va provoquer une erreur � l'ex�cution lorsque ``i`` vaut ``a.length``. Voyez-vous pourquoi ?

- ::

     for(int i=0; i<=b.length;i++) {
      s[i]=a[i]+b[i]; 
     }

  .. class:: comment

     Cette boucle va provoquer une erreur � l'ex�cution lorsque ``i`` vaut ``b.length``. Voyez-vous pourquoi ?

- ::

     for(int i=s.length-1; i>0;i=i-1) {
      s[i]=a[i]+b[i]; 
     }

  .. class:: comment

     Cette boucle ne calculera pas la valeur de ``s[0]``. Voyez-vous pourquoi ?


- ::

     for(int i=s.length; i>=0;i=i-1) {
      s[i]=a[i]+b[i]; 
     }

  .. class:: comment

     Cette boucle va provoquer une erreur � l'ex�cution lorsque ``i`` vaut ``s.length``. Voyez-vous pourquoi ?

Question 11. Tableaux de caract�res
-----------------------------------

La semaine pass�e, vous avez �crit une m�thode ``count`` permettant de d�terminer le nombre d'occurences d'un caract�re dans un ``String``. Lequel des corps ci-dessous est une impl�mentation correcte de la m�thode ``isIn`` dont la sp�cification est ::

 /*
  * @pre cha�ne s non vide
  * @post retourne true si le caract�re c est pr�sent dans la cha�ne s
  *       et false sinon
  */
 public static boolean isIn(char c, char[] s)


.. class:: positive

- ::

    for(int i=0;i<s.length;i++) {
      if(s[i]==c) {
         return true;
      }
    }
    return false;

- ::

    for(int i=s.length-1;i>=0;i=i-1) {
      if(s[i]==c) {
         return true;
      }
    }
    return false;

.. class:: negative

- ::

    for(int i=0;i<s.length();i++) {
      if(s[i]==c) {
         return true;
      }
    }
    return false;

 .. class:: comment

    Le nombre d'�l�ments dans le tableau de caract�re ``s`` est ``s.length`` et non le r�sultat de l'application d'une m�thode ``length()`` qui ne prend pas de param�tre.


- ::

    for(int i=0;i<=s.length;i++) {
      if(s[i]==c) {
         return true;
      }
    }
    return false;

  .. class:: comment

     

- ::

    for(int i=0;i<s.length();i++) {
      if(s[i]==c) {
         return true;
      }
      else {
         return false;
      }
    }

  .. class:: comment

     Que fait cette m�thode apr�s avoir compar� ``c`` avec l'�l�ment ``s[0]`` ?

Question 12. ``toCharArray``
----------------------------


La classe ``String`` contient une m�thode baptis�e `toCharArray() <http://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html#toCharArray()>`_ qui permet de convertir un ``String`` en une cha�ne de caract�res. Une m�thode statique �quivalent pourrait avoir les sp�cification et signature suivantes : ::

 /* 
  * @pre cha�ne s non vide
  * @post retourne un tableau de caract�res ayant le m�me contenu que
  *       que String pass� en param�tre
  */
 public static char[] toCharArray(String s)

Laquelle des s�quences ci-dessous est une impl�mentation correcte de cette m�thode ?


.. class:: positive

- ::

    char[] r=new char[s.length()];
    for(int i=0;i<s.length();i++) {
       r[i]=s.charAt(i);
    }
    return r;

  .. class:: comment
  
     Notez que la longueur d'une cha�ne de caract�res s'obtient en appliquant la m�thode ``length()`` � une r�f�rence vers cette cha�ne. La longueur du tableau de caract�res ``r`` est ``r.length``.

- ::

    char[] r=new char[s.length()];
    for(int i=s.length()-1;i>=0;i=i-1) {
       r[i]=s.charAt(i);
    }
    return r;

  .. class:: comment
  
     Notez que la longueur d'une cha�ne de caract�res s'obtient en appliquant la m�thode ``length()`` � une r�f�rence vers cette cha�ne. La longueur du tableau de caract�res ``r`` est ``r.length``.

.. class:: negative

- ::

   char[] r;
   for(int i=0;i<s.length();i++) {
       r[i]=s.charAt(i);
   }
   return r[];
  
  .. class:: comment

     Cette r�ponse contient deux erreurs. Tout d'abord, avant de pouvoir utiliser un tableau, il faut fixer sa longueur lors de son initialisation. Ensuite, pour retourner un tableau, il faut retourner une r�f�rence vers ce tableau. Si ``r`` est une r�f�rence de type ``char[]``, il suffit de 

- ::

   char[] r=s;
   return r;
  
  .. class:: comment

     En Java, ce genre de raccourci n'existe pas.

- ::

   char[] r=new char[s.length];
   for(int i=0;i<s.length;i++) {
       r[i]=s.charAt(i);
   }
   return r;

  .. class:: comment

     En Java, la longueur d'une cha�ne de caract�res s'obtient via ``s.length()`` et non ``s.length``.


.. include:: ../javanotes_toc.rst
