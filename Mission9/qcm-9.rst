.. Copyright |copy| 2013 Charles Pecheur
.. raw:: html

  <link href="css/prettify.css" type="text/css" rel="stylesheet" />
  <script type="text/javascript" src="js/jquery-1.7.2.min.js"></script>
  <script type="text/javascript" src="js/jquery-shuffle.js"></script>
  <script type="text/javascript" src="js/prettify.js"></script>
  <script type="text/javascript" src="js/rst-form.js"></script>
  <script type="text/javascript">$nmbr_prop = 4</script> 

.. _Arrays : http://docs.oracle.com/javase/1.5.0/docs/api/java/util/Arrays.html
.. |Arrays| replace:: ``java.util.Arrays``
.. _Scanner : http://docs.oracle.com/javase/1.5.0/docs/api/java/util/Scanner.html
.. |Scanner| replace:: ``java.util.Scanner``


===================
Mission 9. Fichiers
===================


Ces questions supposent que vous avez lu les sections suivantes du livre de r�f�rence |jn|_ 

    - |jn3.7|_
        - |jn3.7.1|_
        - |jn3.7.2|_
    - |jn8.1|_
        - |jn8.1.1|_        
        - |jn8.1.2|_        
        - |jn8.1.3|_        
    - |jn8.3|_
        - |jn8.3.1|_        
        - |jn8.3.2|_        
    - |jn11.1|_    
        - |jn11.1.1|_
        - |jn11.1.2|_
        - |jn11.1.3|_
        - |jn11.1.4|_
        - |jn11.1.5|_
    - |jn11.2|_    
        - |jn11.2.1|_
        
ainsi que l'API de la classe |Arrays|_.

Question 1. Erreurs arithm�tiques
---------------------------------

Parmi les affirmations suivantes, laquelle est correcte ?

.. class:: positive

- ``10 / 0`` produit une ``ArithmeticException``.

- ``Integer.MAX_VALUE + 1`` retourne un entier n�gatif.

  .. class:: comment
    
    Le plus petit entier, accessible via ``Integer.MIN_VALUE``.

- ``10.0 / 0.0`` retourne un nombre infini.

  .. class:: comment
    
    C'est une valeur sp�ciale, accessible via ``Double.POSITIVE_INFINITY``.

- ``0.0 / 0.0`` retourne un nombre ind�fini.

  .. class:: comment
    
    C'est une valeur sp�ciale, accessible via ``Double.NaN`` (*Not a Number*).
    
- ``1.0E100 + 1000.0`` retourne ``1.0E100``.

  .. class:: comment
    
    A cause de la pr�cision arithm�tique, ajouter ``1000`` ne change rien � ``1.0E100`` (= $10^{100}$).

.. class:: negative

- ``10 / 0`` provoque toujours l'arr�t du programme.

  .. class:: comment
    
    Ceci cause une ``ArithmeticException`` que l'on peut intercepter et traiter.

- ``Integer.MAX_VALUE + 1`` produit une ``ArithmeticException``.

  .. class:: comment
    
    Les entiers "rebouclent" vers les n�gatifs quand ils d�passent la valeur maximale.
    
- ``10.0 / 0.0`` produit une ``ArithmeticException``.

  .. class:: comment
    
    Les r�els utilisent une valeur sp�ciale ``Double.POSITIVE_INFINITY`` pour repr�senter l'infini.

- ``0.0 / 0.0`` produit une ``ArithmeticException``.

  .. class:: comment
    
    Les r�els utilisent une valeur sp�ciale ``Double.NaN`` (*Not a Number*) pour repr�senter un nombre ind�fini.
    
- ``1.0E100 + 1000.0`` retourne un nombre strictement sup�rieur � ``1.0E100``.

  .. class:: comment
    
    A cause de la pr�cision arithm�tique, ajouter ``1000`` ne change rien � ``1.0E100`` (= :math:`10^{100}`).

Question 2. Traitement des exceptions
-------------------------------------

Quelle d�finition de la m�thode ``toInt`` ci-dessous retourne ``0`` lorsque l'on passe ``"ABC"`` comme param�tre ?

.. class:: positive

- ::

    public static int toInt(String s) {
        try {
            return Integer.parseInt(s);
        } catch (NumberFormatException e) {
            return 0;
        }
    }
        
- ::

    public static int toInt(String s) {
        int n = 0;
        try {
            n = Integer.parseInt(s);
        } catch (NumberFormatException e) {
        }
        return n;
    }
         
  .. class:: comment
         
    Apr�s l'interception de l'exception, l'ex�cution se poursuit apr�s le try-catch.
            
.. class:: negative

- ::

    public static int toInt(String s) {
        int n = Integer.parseInt(s);
        if (n == NumberFormatException) {
            return 0;
        } else {
            return n;
        }
    }

  .. class:: comment
  
    Ceci ne traite pas l'exception.  Utiliser un try-catch.

- ::

    public static int toInt(String s) {
        try {
            return Integer.parseInt(s);
        } catch (NumberFormatException e) {
            System.out.println("Erreur de format");
        }
    }
        
  .. class:: comment
  
    Le traitement de l'exception ne correspond pas � ce qui est demand�.

- ::

    public static int toInt(String s) {
        try {
            return Integer.parseInt(s);
        } catch NumberFormatException {
            return 0;
        }
    }
        
  .. class:: comment
  
    Erreur de syntaxe dans la partie ``catch``.

- ::

    public static int toInt(String s) {
        return Integer.parseInt(s);
        catch (NumberFormatException e) {
            return 0;
        }
    }
        
  .. class:: comment
  
    Il manque le bloc ``try``.

- ::

    public static int toInt(String s) {
        try {
            return Integer.parseInt(s);
        } catch {
            return 0;
        }
    }
        
  .. class:: comment
  
    Erreur de syntaxe dans la partie ``catch``.

Question 3. Traitement des exceptions
-------------------------------------

Soit la m�thode ``m`` suivante ::

    public static int m(int x, int y) {
        try {
            int z = x / y;
            return z;
        } catch (ArithmeticException e) {
            if (x > 0) {
                return x;
            }
        }
        return y;
    }
    
Parmi les ensembles d'affirmations suivantes, lequel est correct ?

.. class:: positive

-

    - ``m(10, 5)`` retourne ``2``
    - ``m(10, 0)`` retourne ``10``
    - ``m(-10, 0)`` retourne ``0``
    
- 

    - ``m(8, 3)`` retourne ``2``
    - ``m(8, 0)`` retourne ``8``
    - ``m(0, 0)`` retourne ``0``

.. class:: negative

-

    - ``m(10, 5)`` retourne ``10``
    - ``m(8, 0)`` retourne ``8``
    - ``m(-10, 0)`` retourne ``0``

    .. class:: comment
  
    Pas d'exception � la premi�re ligne.

-

    - ``m(8, 3)`` retourne ``3``
    - ``m(10, 0)`` retourne ``10``
    - ``m(0, 0)`` retourne ``0``

    .. class:: comment
  
    Pas d'exception � la premi�re ligne.

-

    - ``m(10, 5)`` retourne ``2``
    - ``m(10, 0)`` retourne ``0``
    - ``m(0, 0)`` retourne ``0``

    .. class:: comment
  
    Retourne ``x`` � la deuxi�me ligne.

-

    - ``m(8, 3)`` retourne ``2``
    - ``m(8, 0)`` retourne ``0``
    - ``m(-10, 0)`` retourne ``0``

    .. class:: comment
  
    Retourne ``x`` � la deuxi�me ligne.

-

    - ``m(8, 3)`` retourne ``2``
    - ``m(10, 0)`` retourne ``10``
    - ``m(-10, 0)`` retourne ``-10``

    .. class:: comment
  
    Retourne ``y`` � la troisi�me ligne.

-

    - ``m(10, 5)`` retourne ``2``
    - ``m(10, 0)`` retourne ``10``
    - ``m(0, 0)`` retourne ``1``

    .. class:: comment
  
    Retourne ``y`` � la troisi�me ligne.


Question 4. Classes d'entr�e-sortie
-----------------------------------

Quelles classes sont les plus appropri�es pour lire du texte � partir de ``input.txt`` et �crire du texte vers ``output.txt`` ?

.. class:: positive

- ::

    import java.io.*;
    ...
    BufferedReader inbuf = new BufferedReader(new FileReader("input.txt"));
    PrintWriter outbuf = new PrintWriter(new FileWriter("output.txt")); 

.. class:: negative

- ::

    import java.io.*;
    ...
    BufferedReader inbuf = new BufferedReader("input.txt");
    PrintWriter outbuf = new PrintWriter("output.txt");  

  .. class:: comment
  
    Il n'y a pas de constructeur ``BufferedReader(String filename)``.

- ::

    import java.io.*;
    ...
    BufferedReader inbuf = new BufferedReader(new FileReader("input.txt"));
    BufferedWriter outbuf = new BufferedWriter(new FileWriter("output.txt"));   

  .. class:: comment
  
    ``BufferedWriter`` a des possibilit�s tr�s limit�es, ``PrintWriter`` est plus judicieux.

- ::

    import java.io.*;
    ...
    PrintReader inbuf = new PrintReader(new FileReader("input.txt"));
    PrintWriter outbuf = new PrintWriter(new FileWriter("output.txt"));   

  .. class:: comment
  
    ``PrintReader``` n'existe pas, utilisez ``BufferedReader``.

- ::

    import java.io.*;
    ...
    InputStream inbuf = new InputStream("input.txt");
    OutputStream outbuf = new OutputStream("output.txt");

  .. class:: comment
  
    ``InputStream`` et ``OutputStream`` sont appropri�s pour des donn�es binaires plut�t que pour du texte.

- ::

    import java.io.*;
    ...
    Reader inbuf = new Reader("input.txt");
    Writer outbuf = new Writer("output.txt");   

  .. class:: comment
  
    ``Reader`` et ``Writer`` sont des classes abstraites, utilisez leurs extensions.


Question 5. Lecture de fichier
------------------------------

Parmi les d�finitions de la m�thode ``display`` suivantes, lequel affiche correctement le contenu d'un fichier sur ``System.out`` ?

.. class:: positive

- ::
    
    import java.io.*;
    ...
    public void display(String filename) {
        try {
            BufferedReader buf = 
                new BufferedReader(new FileReader(filename));
            String line = buf.readLine();
            while (line != null) {
                System.out.println(line); 
                line = buf.readLine();
            }
            buf.close();
        } catch (IOException e) {
            System.err.println("Erreur: " + e);
        }
    }

.. class:: negative

- ::

    import java.io.*;
    ...
    public void display(String filename) {
        try {
            BufferedReader buf = 
                new BufferedReader(new FileReader(filename));
            String line = readLine(buf);
            while (line != null) {
                System.out.println(line); 
                line = readLine(buf);
            }
            close(buf);
        } catch (IOException e) {
            System.err.println("Erreur: " + e);
        }
    }

  .. class:: comment
  
    ``readLine`` et ``close`` sont des m�thodes de ``buf``.
    

- ::
    
    import java.io.*;
    ...
    public void display(String filename) {
        try {
            BufferedReader buf = 
                new BufferedReader(new FileReader(filename));
            String line = buf.readLine();
            while (line != null) {
                System.out.println(line); 
                line = buf.readLine();
            }
        } catch (IOException e) {
            System.err.println("Erreur: " + e);
        }
    }

  .. class:: comment
  
    Il faut fermer le flux � la fin.
    
- ::
    
    import java.io.*;
    ...
    public void display(String filename) {
        try {
            BufferedReader buf = 
                new BufferedReader(new FileReader(filename));
            String line = buf.readLine();
            while (line != "") {
                System.out.println(line); 
                line = buf.readLine();
            }
            buf.close();
        } catch (IOException e) {
            System.err.println("Erreur: " + e);
        }
    }

  .. class:: comment
  
    Le test de boucle est incorrect.

- ::
    
    import java.io.*;
    ...
    public void display(String filename) {
        try {
            BufferedReader buf = 
                new BufferedReader(new FileReader(filename));
            String line = buf.readLine();
            while (line != null) {
                System.out.println(line); 
            }
            buf.close();
        } catch (IOException e) {
            System.err.println("Erreur: " + e);
        }
    }

  .. class:: comment
  
    Seule la premi�re ligne du fichier est lue.

- ::
    
    import java.io.*;
    ...
    public void display(String filename) {
        BufferedReader buf = 
            new BufferedReader(new FileReader(filename));
        String line = buf.readLine();
        while (line != null) {
            System.out.println(line); 
            line = buf.readLine();
        }
        buf.close();
    }

  .. class:: comment
  
    Il manque la gestion des exceptions.
    
- ::
    
    import java.io.*;
    ...
    public void display(String filename) {
        try {
            BufferedReader buf = 
                new BufferedReader(new FileReader(filename));
            String line;
            while (line != null) {
                line = buf.readLine();
                System.out.println(line); 
            }
            buf.close();
        } catch (IOException e) {
            System.err.println("Erreur: " + e);
        }
    }

  .. class:: comment
  
    La gestion de la variable ``line`` est incorrecte, la boucle ne sera jamais ex�cut�e.
    
Question 6. La classe ``Scanner``
---------------------------------

Consid�rons un fichier ``numbers.txt`` qui contient des nombres entiers s�par�s par des espaces, par exemple ::

    1 2 3 4
    1 10 100
    1348

Quel fragment de programme utilise correctement un ``Scanner`` (voir |Scanner|_) pour imprimer la somme de ces nombres ?

.. class:: positive

- ::

    import java.util.Scanner;
    ...
    try {
        Scanner scan = 
            new Scanner(new java.io.FileReader("numbers.txt"));
        int sum = 0;
        while (scan.hasNextInt()) {
            sum = sum + scan.nextInt();
        }
        scan.close();
        System.out.println(sum);
    } catch (IOException e) {
        System.err.println("Erreur: " + e);
    }

.. class:: negative

- ::

    import java.io.Scanner;
    ...
    try {
        Scanner scan = 
            new Scanner(new java.io.FileReader("numbers.txt"));
        int sum = 0;
        while (scan.hasNextInt()) {
            sum = sum + scan.nextInt();
        }
        scan.close();
        System.out.println(sum);
    } catch (IOException e) {
        System.err.println("Erreur: " + e);
    }

  .. class:: comment
  
    ``Scanner`` est dans le package ``java.util``.

- ::

    import java.util.Scanner;
    ...
    try {
        Scanner scan = 
            new Scanner("numbers.txt");
        int sum = 0;
        while (scan.hasNextInt()) {
            sum = sum + scan.nextInt();
        }
        scan.close();
        System.out.println(sum);
    } catch (IOException e) {
        System.err.println("Erreur: " + e);
    }

  .. class:: comment
  
    Il n'y a pas de constructeur ``Scanner(String filename)``.  Utiliser un ``FileReader``.

- ::

    import java.util.Scanner;
    ...
    try {
        Scanner scan = 
            new Scanner(new java.io.FileReader("numbers.txt"));
        int sum = 0;
        while (!scan.eof()) {
            sum = sum + scan.nextInt();
        }
        scan.close();
        System.out.println(sum);
    } catch (IOException e) {
        System.err.println("Erreur: " + e);
    }

  .. class:: comment
  
    ``Scanner`` n'a pas de m�thode ``eof``.  Utiliser ``hasNextInt``.

- ::

    import java.util.Scanner;
    ...
    try {
        Scanner scan = 
            new Scanner(new java.io.FileReader("numbers.txt"));
        int sum = 0;
        while (hasNextInt(scan)) {
            sum = sum + nextInt(scan);
        }
        scan.close();
        System.out.println(sum);
    } catch (IOException e) {
        System.err.println("Erreur: " + e);
    }

  .. class:: comment
  
    ``hasNextInt`` et ``nextInt`` sont des m�thodes de ``scan``.


Question 7. M�thodes de comparaison
-----------------------------------

On d�sire trier et faire des recherches sur un tableau contenant des objets qui repr�sentent des �tudiants (``Student[]``) � l'aide des m�thodes de la classe |Arrays|_.  Quelles interfaces et m�thodes la classe ``Student`` doit-elle impl�menter ?

.. class:: positive

- ::

    public class Student implements Comparable {
        ...
        public boolean equals(Object o) { ... }
        public int compareTo(Object o) { ... }
    }

.. class:: negative

- ::

    public class Student {
        ...
        public boolean equals(Object o) { ... }
        public int compareTo(Object o) { ... }
    }

  .. class:: comment
  
    Il faut d�clarer qu'on impl�mente l'interface ``Comparable``.

- ::

    public class Student implements Comparable {
        ...
        public boolean equals(Student stud) { ... }
        public int compareTo(Student stud) { ... }
    }

  .. class:: comment
  
    Les m�thodes ``equals`` et ``compareTo`` doivent prendre un ``Object`` en param�tre.

- ::

    public class Student implements Comparable {
        ...
        public boolean equals(Object o) { ... }
        public boolean greater(Object o) { ... }
        public boolean less(Object o) { ... }
    }

  .. class:: comment
  
    Ce ne sont pas les bonnes m�thodes pour ``Comparable``.

- ::

    public class Student implements Equality, Comparable {
        ...
        public boolean equals(Object o) { ... }
        public int compareTo(Object o) { ... }
    }

  .. class:: comment
  
    Il n'y a pas d'interface ``Equality``; ``equals`` est une m�thode de ``Object``.

Question 8. La classe ``Arrays``
--------------------------------

Etant donn� un tableau non-tri� d'�tudiants ``Student[] groupe`` et un �tudiant ``Student stud``, comment v�rifier si ``stud`` appartient � ``groupe`` en utilisant les m�thodes de la classe |Arrays|_, en supposant que ``Student`` impl�mente les interfaces et m�thodes mentionn�es � la question 7 ?

.. class:: positive

- ::

    import java.util.Arrays;
    ...
    public static void contains(Student[] groupe, Student stud) {
        Arrays.sort(groupe);
        int index = Arrays.binarySearch(groupe, stud);
        return stud.equals(groupe[index]);
    }

.. class:: negative

- ::

    import java.util.Arrays;
    ...
    public static boolean contains(Student[] groupe, Student stud) {
        groupe.sort();
        int index = groupe.binarySearch(stud);
        return stud.equals(groupe[index]);
    }

  .. class:: comment
  
    ``sort`` et ``binarySearch`` sont des m�thodes de classe de ``Arrays``.
    
- ::

    import java.util.Arrays;
    ...
    public static boolean contains(Student[] groupe, Student stud) {
        Student[] sorted = Arrays.sort(groupe);
        int index = Arrays.binarySearch(sorted, stud);
        return stud.equals(groupe[index]);
    }

  .. class:: comment
  
    ``binarySearch`` ne retourne pas de r�sultat, elle modifie le tableau.
    
- ::

    import java.util.Arrays;
    ...
    public static boolean contains(Student[] groupe, Student stud) {
        Arrays.sort(groupe);
        return Arrays.binarySearch(groupe, stud);
    }

  .. class:: comment
  
    ``binarySearch`` retourne un indice, pas un bool�en.

- ::

    import java.util.Arrays;
    ...
    public static boolean contains(Student[] groupe, Student stud) {
        int index = Arrays.binarySearch(groupe, stud);
        return stud.equals(groupe[index]);
    }

  .. class:: comment
  
    ``binarySearch`` ne fonctionne que sur un tableau tri�.

- ::

    import java.util.Arrays;
    ...
    public static boolean contains(Student[] groupe, Student stud) {
        Arrays.sort(groupe);
        int index = Arrays.binarySearch(groupe, stud);
        return stud == groupe[index];
    }

  .. class:: comment
  
    La comparaison dans le ``return`` ne convient pas, on compare des r�f�rences.

.. =================================================
.. include:: ../javanotes_toc.rst
