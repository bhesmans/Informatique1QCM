.. Copyright |copy| 2013 Charles Pecheur

.. raw:: html

  <link href="css/prettify.css" type="text/css" rel="stylesheet" />
  <script type="text/javascript" src="js/jquery-1.7.2.min.js"></script>
  <script type="text/javascript" src="js/jquery-shuffle.js"></script>
  <script type="text/javascript" src="js/prettify.js"></script>
  <script type="text/javascript" src="js/rst-form.js"></script>
  <script type="text/javascript">$nmbr_prop = 4</script> 

.. _TextIO : http://math.hws.edu/eck/cs124/javanotes6/source/TextIO.java
.. |TextIO| replace:: ``TextIO``


================================
Mission 7. Extension et H�ritage
================================


Ces questions supposent que vous avez lu les sections suivantes du livre de r�f�rence |jn|_ 

  - |jn2.4|_
  
    - |jn2.4.4|_
    
  - |jn4.3|_

    - |jn4.3.3|_
    
  - |jn5.3|_

    - |jn5.3.3|_

  - |jn5.5|_

    - |jn5.5.1|_
    - |jn5.5.2|_
    - |jn5.5.3|_
    - |jn5.5.4|_

  - |jn5.6|_

    - |jn5.6.1|_
    - |jn5.6.2|_
    - |jn5.6.3|_
    
  - |jn5.7|_
  
    - |jn5.7.4|_
     

Question 1. H�ritage : vocabulaire
----------------------------------

Si la classe ``C3`` �tend la classe ``C2``, qui �tend elle-m�me la classe ``C1``, quel groupe d'affirmations est correct ?

.. class:: positive

-

    - ``C1`` est une super-classe de ``C3``
    - ``C2`` est une classe-fille de ``C1``
    - Toute instance de ``C3`` est une instance de ``C1``

-

    - ``C3`` est une sous-classe de ``C2``
    - ``C2`` est la classe-m�re de ``C3``
    - Toute instance de ``C2`` est une instance de ``C1``

.. class:: negative

-

    - ``C1`` est une sous-classe de ``C3``
    - ``C2`` est une classe-fille de ``C1``
    - Toute instance de ``C2`` est une instance de ``C1``

    .. class:: comment
    
    ``C1`` n'est pas une sous-classe de ``C3``.

-

    - ``C1`` est une super-classe de ``C3``
    - ``C2`` est une classe-fille de ``C3``
    - Toute instance de ``C3`` est une instance de ``C1``

    .. class:: comment
    
    ``C2`` n'est pas une classe-fille de ``C3``.

-

    - ``C2`` est une classe-fille de ``C1``
    - Toute instance de ``C1`` est une instance de ``C3``
    - ``C3`` est une sous-classe de ``C2``

    .. class:: comment
    
    Toute instance de ``C1`` n'est pas une instance de ``C3``.
    
-

    - ``C2`` est une classe-fille de ``C1``
    - Toute instance de ``C3`` est une instance de ``C1``
    - ``C1`` est une sous-classe de ``C2``

    .. class:: comment
    
    ``C1`` n'est pas une sous-classe de ``C2``

-

    - ``C1`` est une super-classe de ``C3``
    - ``C2`` est la classe-fille de ``C3``
    - Toute instance de ``C2`` est une instance de ``C1``

    .. class:: comment
    
    ``C2`` n'est pas la classe-fille de ``C3``

-

    - ``C2`` est une classe-fille de ``C1``
    - ``C3`` est une sous-classe de ``C2``
    - Toute instance de ``C2`` est une instance de ``C3``

    .. class:: comment
    
    Toute instance de ``C2`` n'est pas une instance de ``C3``
    
Question 2. Extension de classe
-------------------------------

Soit la classe ``C1`` d�finie comme suit ::

    public class C1 {
        private String s;
        private int n;
        public C1(String s, int n) {
            this.s = s;
            this.n = n;
        }
        public int m() {
            return n * n;
        }
    }
    
Laquelle des d�finitions suivantes d�finit correctement une extension de ``C1`` ? 

.. class:: positive

- ::

    public class C2 extends C1 {
        private int n2;
        public C2 (String s, int n) {
            super(s, n);
            this.n2 = n;
        }
        public int m() {
            return super.m() + n2 * n2;
        }
    }

.. class:: negative

- ::

    public class C2 extends C1 {
        private int n2;
        public C2 (String s, int n) {
            C1(s, n);
            this.n2 = n;
        }
        public int m() {
            return C2.m() + n2 * n2;
        }
    }

  .. class:: comment

    Il faut utiliser ``super`` pour r�f�rer � la classe-m�re et non ``C2``.

- ::

    public class C2 {
        private int n2;
        public C2 (String s, int n) {
            super(s, n);
            this.n2 = n;
        }
        public int m() {
            return super.m() + n2 * n2;
        }
    }

  .. class:: comment

    La d�claration ne mentionne pas que ``C2`` �tend ``C1``.

- ::

    public class C2 extends C1 {
        private int n2;
        public C2 (String s, int n) {
            super(s, n);
            this.n2 = n;
        }
        public override int m() {
            return super.m() + n2 * n2;
        }
    }

  .. class:: comment

    Dans la signature de ``m``, le ``override`` est incorrect et inutile (il existe une annotation ``@override`` mais elle n'est pas indispensable).

- ::

    public class C2 extends C1 {
        private int n2;
        public C2 (String s, int n) {
            super(s, n);
            this.n2 = n;
        }
        public int m() {
            return n1 * n1 + n2 * n2;
        }
    }
    
  .. class:: comment

    Dans le corps de ``m``, la variable ``n`` de ``C1`` n'est pas accessible (``private``).

- ::

    public class C2 extends C1 {
        private int n2;
        public C2 (String s, int n) {
            this.s = s;
            this.n = n;
            this.n2 = n;
        }
        public int m() {
            return super.m() + n2 * n2;
        }
    }

  .. class:: comment

    Dans le constructeur de ``C2``, il faut appeler le constructeur de ``C1`` pour initialiser les variables de ``C1``.
    

- ::

    public class C2 extends C1 {
        private int n2;
        public C2 (String s, int n) {
            this.n2 = n;
            super(s, n);
        }
        public int m() {
            return super.m() + n2 * n2;
        }
    }

  .. class:: comment
  
      Dans le constructeur, l'appel au constructeur de ``C1`` doit venir en premier lieu.

Question 3. Extension et types
------------------------------

Soit les classes ``C1``, ``C2``, ``C3`` et ``C4`` d�finies comme suit ::

    public class C1 {
        public C1() {
            // ...
        }
        // ...
    }

    public class C2 extends C1 {
        public C2() {
            // ...
        }
        // ...
    }

    public class C3 extends C2 {
        public C3() {
            // ...
        }
        // ...
    }

    public class C4 extends C2 {
        public C4() {
            // ...
        }
        // ...
    }

Parmi les portions de code suivantes, laquelle est valide pour le compilateur Java ?

.. class:: positive

- ::

    C3 obj3 = new C3();
    C2 obj2 = new C3();
    C4 obj4 = new C4();
    C1 obj1 = obj3;
  
- ::

    C4 obj4 = new C4();
    C2 obj2 = obj4;
    C1 obj1 = new C2();
    C3 obj3 = null;

.. class:: negative

- ::

    C4 obj4 = new C4();
    C3 obj3 = new C2();
    C2 obj2 = new C3();
    C1 obj1 = obj3;

  .. class:: comment
  
    ``C3 obj3`` ne peut pas recevoir une expression de type ``C2``.

- ::

    C3 obj3 = new C3();
    C2 obj2 = new C3();
    C1 obj1 = obj3;
    C4 obj4 = obj2;

  .. class:: comment

    ``C4 obj4`` ne peut pas recevoir une expression de type ``C2``.

- ::

    C4 obj4 = new C4();
    C3 obj3 = new C3();
    C1 obj1 = obj3;
    C2 obj2 = obj1;

  .. class:: comment

    ``C2 obj2`` ne peut pas recevoir une expression de type ``C1`` (m�me si l'objet qu'elle d�signe est en fait de type ``C3``).

- ::

    C3 obj3 = null;
    C2 obj2 = obj4;
    C4 obj4 = obj3;
    C1 obj1 = new C2();

  .. class:: comment

    ``C4 obj4`` ne peut pas recevoir une expression de type ``C3`` (m�me si elle produit la r�f�rence ``null``).

- ::

    C4 obj4 = new C4();
    C2 obj2 = obj4;
    C3 obj3 = new C1();
    C1 obj1 = new C2();

  .. class:: comment

    ``C3 obj3`` ne peut pas recevoir une expression de type ``C1``.

- ::

    C2 obj2 = new C3();
    C1 obj1 = new C2();
    C3 obj3 = obj2;
    C4 obj4 = new C4();

  .. class:: comment

    ``C3 obj3`` ne peut pas recevoir une expression de type ``C3`` (m�me si l'objet qu'elle d�signe est en fait de type ``C3``).
     
Question 4. Conversions de type
-------------------------------

Soit les classes ``C1`` et ``C2`` d�finies comme suit ::

    public class C1 {
        public C1() {
            // ...
        }
        // ...
    }

    public class C2 extends C1 {
        public C2() {
            // ...
        }
        // ...
    }

On consid�re ensuite les instructions suivantes ::

    C1 obj1 = new C1();
    C2 obj2 = new C2();
    C1 obj3 = new C2();

    C2 conv12 = obj1;
    C1 conv21 = obj2;
    C2 conv32 = obj3;
    C2 cast12 = (C2) obj1;
    C1 cast21 = (C1) obj2;
    C2 cast32 = (C2) obj3;
    
Parmi ces instructions, certaines causent une erreur � le compilation ou � l'ex�cution.  Parmi les propositions ci-dessous, laquelle identifie correctement ces erreurs ?

.. class:: positive

- ::

    C2 conv12 = obj1;       // => erreur � la compilation
    C1 conv21 = obj2;       // => OK
    C2 conv32 = obj3;       // => erreur � la compilation
    C2 cast12 = (C2) obj1;  // => erreur � l'ex�cution
    C1 cast21 = (C1) obj2;  // => OK mais type-cast inutile
    C2 cast32 = (C2) obj3;  // => OK

.. class:: negative

- ::

    C2 conv12 = obj1;       // => erreur � la compilation
    C1 conv21 = obj2;       // => OK
    C2 conv32 = obj3;       // => OK
    C2 cast12 = (C2) obj1;  // => erreur � l'ex�cution
    C1 cast21 = (C1) obj2;  // => OK mais type-cast inutile
    C2 cast32 = (C2) obj3;  // => OK

  .. class:: comment
  
    La variable ``obj3`` est de type ``C1`` : erreur de compilation � la ligne 3.

- ::

    C2 conv12 = obj1;       // => erreur � la compilation
    C1 conv21 = obj2;       // => OK
    C2 conv32 = obj3;       // => erreur � la compilation
    C2 cast12 = (C2) obj1;  // => OK
    C1 cast21 = (C1) obj2;  // => OK mais type-cast inutile
    C2 cast32 = (C2) obj3;  // => OK

  .. class:: comment
  
    ``obj1`` r�f�re � une instance de ``C1`` : erreur de type-cast � l'ex�cution � la ligne 4.

- ::

    C2 conv12 = obj1;       // => erreur � la compilation
    C1 conv21 = obj2;       // => OK
    C2 conv32 = obj3;       // => erreur � la compilation
    C2 cast12 = (C2) obj1;  // => erreur � l'ex�cution
    C1 cast21 = (C1) obj2;  // => OK mais type-cast inutile
    C2 cast32 = (C2) obj3;  // => erreur � l'ex�cution

  .. class:: comment
  
    ``obj3`` r�f�re bien � une instance de ``C2`` : pas d'erreur � la ligne 6.

- ::

    C2 conv12 = obj1;       // => erreur � la compilation
    C1 conv21 = obj2;       // => OK
    C2 conv32 = obj3;       // => erreur � la compilation
    C2 cast12 = (C2) obj1;  // => erreur � la compilation
    C1 cast21 = (C1) obj2;  // => OK mais type-cast inutile
    C2 cast32 = (C2) obj3;  // => OK

  .. class:: comment
  
    La ligne 4 est correcte du point de vue des types mais causera erreur de type-cast � l'ex�cution.

- ::

    C2 conv12 = obj1;       // => erreur � la compilation
    C1 conv21 = obj2;       // => erreur � la compilation
    C2 conv32 = obj3;       // => erreur � la compilation
    C2 cast12 = (C2) obj1;  // => erreur � l'ex�cution
    C1 cast21 = (C1) obj2;  // => OK mais type-cast inutile
    C2 cast32 = (C2) obj3;  // => OK

  .. class:: comment
  
    La variable ``obj2`` est de type ``C2`` qui est une sous-classe de ``C1`` : pas d'erreur � la ligne 2.

- ::

    C2 conv12 = obj1;       // => erreur � la compilation
    C1 conv21 = obj2;       // => OK
    C2 conv32 = obj3;       // => erreur � la compilation
    C2 cast12 = (C2) obj1;  // => erreur � l'ex�cution
    C1 cast21 = (C1) obj2;  // => erreur � l'ex�cution
    C2 cast32 = (C2) obj3;  // => OK

  .. class:: comment
  
    ``obj2`` r�f�re � une instance de ``C2`` qui est bien une sous-classe de ``C1`` : pas d'erreur � la ligne 5.

Question 5. Re-d�finition et surcharge
--------------------------------------


Soit les classes ``C1`` et ``C2`` d�finies comme suit ::

    public class C1 {
        // ...
        public int m1(String s, int n) {
            // ...
        }
    }

    public class C2 extends C1 {
        // ...
    }

Parmi les d�finitions suivantes dans ``C2``, laquelle constitue une *re-d�finition* (overriding) correcte de la m�thode ``m1`` de la classe ``C1`` et non une *surcharge* (overloading) ?

.. class:: positive

- ::

        public int m1(String s, int n) {
            return super.m1(s, n * 2) + 10;
        }

- ::

        public int m1(String x, int i) {
            return super.m1(x, i * 2) + 10;
        }

  .. class:: comment

    Les param�tres peuvent avoir un nom diff�rent, pour autant que types correspondent exactement.
    
.. class:: negative

- ::

        public int m1(int n, String s) {
            return super.m1(s, n * 2) + 10;
        }

  .. class:: comment
  
    Les param�tres doivent �tre dans le m�me ordre.

- ::

        public double m1(String s, int n) {
            return super.m1(s, n * 2) + 10.0;
        }

  .. class:: comment
  
    Le type de r�sultat doit �tre le m�me.

- ::

        public int m1(String s, int n) {
            return super(s, n * 2) + 10;
        }

  .. class:: comment
  
    Erreur de syntaxe : utiliser ``super.m1`` pour appeler la m�thode ``m1`` de la classe-m�re.

- ::

        public int m1(String s, int n, int n2) {
            return super.m1(s, n * 2) + n2;
        }

  .. class:: comment
  
    Il faut conserver le m�me nombre de param�tres.
    
Question 6. Modificateurs de visibilit�
---------------------------------------

Consid�rez les classes ``C1``, ``C2``, ``C3`` d�finies comme suit ::

    public class C1 {
        // ...
        public    int publ() { /* ... */ }
        protected int prot() { /* ... */ }
        private   int priv() { /* ... */ }
        public int m1() { /* ... */ }
    }

    public class C2 extends C1 {
        // ...
        public int m2() { /* ... */ }
    }
    
    public class C3 {
        // ...
        public int m3() { /* ... */ }
    }

Parmi les groupes d'affirmation suivants, lequel est correct ?

.. class:: positive

-

    - ``publ`` peut �tre appel�e dans le corps de ``m3``.
    - ``prot`` peut �tre appel�e dans le corps de ``m2``.
    - ``priv`` NE peut PAS �tre appel�e dans le corps de ``m2``.

-

    - ``publ`` peut �tre appel�e dans le corps de ``m2``.
    - ``prot`` NE peut PAS �tre appel�e dans le corps de ``m3``.
    - ``priv`` peut �tre appel�e dans le corps de ``m1``.

.. class:: negative

-

    - ``publ`` NE peut PAS �tre appel�e dans le corps de ``m3``.
    - ``prot`` peut �tre appel�e dans le corps de ``m2``.
    - ``priv`` peut �tre appel�e dans le corps de ``m1``.

    .. class:: comment
  
    ``publ`` a la visibilit� ``public``, elle peut �tre appel�e partout.

-

    - ``publ`` peut �tre appel�e dans le corps de ``m3``.
    - ``prot`` NE peut PAS �tre appel�e dans le corps de ``m2``.
    - ``priv`` peut �tre appel�e dans le corps de ``m1``.

    .. class:: comment
  
    ``prot`` a la visibilit� ``protected``, elle peut �tre appel�e dans la classe ``C2`` qui �tend ``C1``.

-

    - ``priv`` peut �tre appel�e dans le corps de ``m2``.
    - ``publ`` peut �tre appel�e dans le corps de ``m2``.
    - ``prot`` NE peut PAS �tre appel�e dans le corps de ``m3``.

    .. class:: comment
  
    ``priv`` a la visibilit� ``private``, elle peut �tre appel�e uniquement dans sa propre classe ``C1``.

-

    - ``prot`` peut �tre appel�e dans le corps de ``m2``.
    - ``publ`` NE peut PAS �tre appel�e dans le corps de ``m2``.
    - ``priv`` peut �tre appel�e dans le corps de ``m1``.

    .. class:: comment
  
    ``publ`` a la visibilit� ``public``, elle peut �tre appel�e partout.

-

    - ``publ`` peut �tre appel�e dans le corps de ``m3``.
    - ``prot`` peut �tre appel�e dans le corps de ``m3``.
    - ``priv`` peut �tre appel�e dans le corps de ``m1``.

    .. class:: comment
  
    ``prot`` a la visibilit� ``protected``, elle ne peut pas �tre appel�e dans ``C3`` qui n'�tend pas ``C1``.

-

    - ``publ`` peut �tre appel�e dans le corps de ``m3``.
    - ``prot`` peut �tre appel�e dans le corps de ``m2``.
    - ``priv`` NE peut PAS �tre appel�e dans le corps de ``m1``.

    .. class:: comment
  
    ``priv`` peut toujours �tre appel�e dans la classe o� elle est d�finie.
        
Question 7. Variables et m�thodes de classe
-------------------------------------------

On consid�re le code suivant ::

    public class C {
        private static int svar;
        private int var;
        
        public void m1() { var = var + 1; }
        public void m2() { svar = svar + 1; }
        public static void m3() { var = var + 1; }
        public static void m4() { svar = svar + 1; }
    }

Parmi ces d�finitions de m�thode, lesquelles produisent une erreur de compilation ?

.. class:: positive

- La m�thode ``m3``
      
  .. class:: comment
    
    Une m�thode de classe (``static``) ne peut pas acc�der � la variable d'instance ``var``.
    
.. class:: negative

- Les m�thodes ``m2`` et ``m3``

  .. class:: comment

    ``m2`` peut parfaitement acc�der � la variable de classe ``svar``.

- Les m�thodes ``m3`` et ``m4``

  .. class:: comment

    ``m4`` est parfaitement valide.

- La m�thode ``m2``

  .. class:: comment

    ``m2`` peut parfaitement acc�der � la variable de classe ``svar``.

- La m�thode ``m4``        

  .. class:: comment

    ``m4`` est parfaitement valide.

- Aucune

  .. class:: comment

    La m�thode de classe (``static``) ``m3`` ne peut pas acc�der � la variable d'instance ``var``.

Question 8. Variables de classe et d'instance
---------------------------------------------

On consid�re la classe ``C`` suivante ::

    public class C {
        private static int svar = 0;
        private int var;
        
        public C() {
            var = 0;
        }
        
        public void m1() { 
            var = var + 1; 
            System.out.println(var);
        }
        
        public void m2() { 
            svar = svar + 10;
            System.out.println(svar);
        }
    }

On ex�cute les instructions suivantes :: 

    C c1 = new C();
    c1.m1();
    c1.m2();
    C c2 = new C();
    c2.m1();
    c2.m2();
    
Quel est le r�sultat affich� ?

.. class:: positive

- ::

    1
    10
    1
    20
    
  .. class:: comment
    
    ``m1`` affecte des variables d'instance distinctes de ``c1`` et ``c2`` tandis que ``m2`` affecte une variable de classe commune.
    
.. class:: negative

- ::

    1
    10
    1
    10
    
  .. class:: comment
    
    ``m2`` affecte une variable de classe commune.
    
- ::

    1
    10
    2
    20
    
  .. class:: comment
    
    ``m1`` affecte des variables d'instance distinctes de ``c1`` et ``c2``.

- ::

    1
    11
    12
    22
    
  .. class:: comment
    
    ``m1`` et ``m2`` affectent des variables diff�rentes ``var`` et ``svar``

- ::

    1
    2
    1
    2
    
  .. class:: comment
    
    Attention, on appelle deux m�thodes diff�rentes ``m1`` et ``m2``.
    

Question 9. La m�thode ``equals``
---------------------------------

Soit la classe ``Point`` d�finie comme suit ::

    public class Point {
        private int x;
        private int y;
        public C1(int x, int y) {
            this.x = x;
            this.y = y;
        }
        // ...
    }
    
Dans cette classe, laquelle des d�finitions suivantes re-d�finirait correctement la m�thode ``equals`` de la classe ``Object`` ? 

.. class:: positive

- ::

    public boolean equals(Object other) {
        if (other != null && other instanceof Point) {
            Point p = (Point) other;
            return ((this.x == p.x) && (this.y == p.y));
        } else {
            return false;
        }
    }

.. class:: negative

- ::

    public boolean equals(Object other) {
        if (other != null && other instanceof Point) {
            return ((this.x == other.x) && (this.y == other.y));
        } else {
            return false;
        }
    }
    
  .. class:: comment
  
    ``other`` est de type ``Object``, ``other.x`` n'est pas correct.
    
- ::

    public boolean equals(Object other) {
        if (other instanceof Point) {
            Point p = (Point) other;
            return ((this.x == p.x) && (this.y == p.y));
        } else {
            return false;
        }
    }
    
  .. class:: comment
  
    ``other`` pourrait �tre ``null``.
    
- ::

    public boolean equals(Point other) {
        return ((this.x == other.x) && (this.y == other.y));
    }
    
  .. class:: comment
  
    Ceci fonctionne mais ne correspond pas � la m�thode ``equals`` de ``Object``.  Le param�tre doit �tre de type ``Object``.
    
- ::

    public boolean equals(Object other) {
        Point p = (Point) other;
        return ((this.x == p.x) && (this.y == p.y));
    }
    
  .. class:: comment
  
    Ceci produira une erreur � l'ex�cution si ``other`` est ``null`` ou n'est pas de type ``Point``.

.. =================================================
.. include:: ../javanotes_toc.rst
