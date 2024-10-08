## Trabajo de desarrollo e investigación
## Nombre: Efrain Vitorino Marin
## Codigo: 160337
-------------------------
# 1. Desarrolle una aplicación para conjuntos, utilizando la estructura estática de arreglos
- # Visión del Conceptor
- Nombre de la clase: `CConjunto`


Un conjunto es una colección de elementos únicos, en este caso números enteros. Las operaciones básicas que se pueden realizar con estos conjuntos incluyen:
- Unión: Combina todos los elementos de dos conjuntos sin duplicados.
- Intersección: Obtiene los elementos comunes entre dos conjuntos.
- Diferencia: Devuelve los elementos que están en el primer conjunto pero no en el segundo.
- Diferencia Simétrica: Devuelve los elementos que están en uno de los conjuntos pero no en ambos.

## Atributos:
   - `aElementos`: Arreglo de enteros que almacena los elementos únicos del conjunto.
   - `aNroElementos`: Entero que indica el número actual de elementos en el conjunto.
   - `aMaxSize`: Constante que define el tamaño máximo del conjunto (100 en este caso).
## Constructores:
   - `Conjunto()`: Inicializa el conjunto vacío.
   - `Conjunto(int[] pElementos)`: Inicializa el conjunto con los elementos proporcionados en el arreglo `pElementos`, eliminando duplicados si es necesario.
## Métodos:
- `Agregar(int elemento)`: Añade un elemento al conjunto si no está presente y si hay espacio disponible.
- `Contiene(int elemento)`: Verifica si un elemento está en el conjunto.
- `Union(CConjunto otro)`: Devuelve un nuevo conjunto que contiene todos los elementos de ambos conjuntos, sin duplicados.
 - `Interseccion(CConjunto otro)`: Devuelve un nuevo conjunto que contiene los elementos comunes entre los dos conjuntos.
- `Diferencia(CConjunto otro)`: Devuelve un nuevo conjunto que contiene los elementos que están en el primer conjunto pero no en el segundo.
- `DiferenciaSimetrica(CConjunto otro)`: Devuelve un nuevo conjunto que contiene los elementos que están en uno de los conjuntos, pero no en ambos.
- `MostrarConjunto()`: Imprime los elementos del conjunto en la consola en un formato legible.
## Codigo completo en C#
```C#
using System;

namespace AppConjuntoArreglo
{
    internal class Program
    {
        static void Main(string[] args)
        {
            // Inicialización de conjuntos con arreglos de prueba
            int[] A = { 3, 6, 4, 1, 2 };
            Conjunto C1 = new Conjunto(A);
            int[] B = { 1, 2, 5, 7, 6 };
            Conjunto C2 = new Conjunto(B);
            
            Console.WriteLine("Conjunto A:");
            C1.MostrarConjunto();
            
            Console.WriteLine("Conjunto B:");
            C2.MostrarConjunto();
            
            // Operación de Unión
            Conjunto unionConjunto = C1.Union(C2);
            Console.WriteLine("Unión de A y B:");
            unionConjunto.MostrarConjunto();
            
            // Operación de Intersección
            Conjunto interseccionConjunto = C1.Interseccion(C2);
            Console.WriteLine("Intersección de A y B:");
            interseccionConjunto.MostrarConjunto();
            
            // Operación de Diferencia (A - B)
            Conjunto diferenciaConjunto = C1.Diferencia(C2);
            Console.WriteLine("Diferencia de A y B (A - B):");
            diferenciaConjunto.MostrarConjunto();
            
            // Operación de Diferencia Simétrica
            Conjunto diferenciaSimetricaConjunto = C1.DiferenciaSimetrica(C2);
            Console.WriteLine("Diferencia Simétrica de A y B:");
            diferenciaSimetricaConjunto.MostrarConjunto();

            Console.ReadKey();
        }
    }

    public class Conjunto
    {
        // Atributos
        private int[] aElementos;
        private int aNroElementos;
        private const int aMaxSize = 100;

        // Constructores
        public Conjunto()
        {
            aElementos = new int[aMaxSize];
            aNroElementos = 0;
        }

        public Conjunto(int[] pElementos)
        {
            aElementos = new int[aMaxSize];
            aNroElementos = 0;
            for (int i = 0; i < pElementos.Length; i++)
            {
                Agregar(pElementos[i]);
            }
        }

        // Métodos
        public void Agregar(int elemento)
        {
            if (!Contiene(elemento) && aNroElementos < aMaxSize)
            {
                aElementos[aNroElementos] = elemento;
                aNroElementos++;
            }
        }

        public bool Contiene(int elemento)
        {
            for (int i = 0; i < aNroElementos; i++)
            {
                if (aElementos[i] == elemento)
                    return true;
            }
            return false;
        }

        public Conjunto Union(Conjunto otroConjunto)
        {
            Conjunto resultado = new Conjunto();
            for (int i = 0; i < aNroElementos; i++)
            {
                resultado.Agregar(aElementos[i]);
            }

            for (int i = 0; i < otroConjunto.aNroElementos; i++)
            {
                resultado.Agregar(otroConjunto.aElementos[i]);
            }

            return resultado;
        }

        public Conjunto Interseccion(Conjunto otroConjunto)
        {
            Conjunto resultado = new Conjunto();
            for (int i = 0; i < aNroElementos; i++)
            {
                if (otroConjunto.Contiene(aElementos[i]))
                {
                    resultado.Agregar(aElementos[i]);
                }
            }
            return resultado;
        }

        public Conjunto Diferencia(Conjunto otroConjunto)
        {
            Conjunto resultado = new Conjunto();
            for (int i = 0; i < aNroElementos; i++)
            {
                if (!otroConjunto.Contiene(aElementos[i]))
                {
                    resultado.Agregar(aElementos[i]);
                }
            }
            return resultado;
        }

        public Conjunto DiferenciaSimetrica(Conjunto otroConjunto)
        {
            Conjunto resultado = new Conjunto();
            for (int i = 0; i < aNroElementos; i++)
            {
                if (!otroConjunto.Contiene(aElementos[i]))
                {
                    resultado.Agregar(aElementos[i]);
                }
            }

            for (int i = 0; i < otroConjunto.aNroElementos; i++)
            {
                if (!Contiene(otroConjunto.aElementos[i]))
                {
                    resultado.Agregar(otroConjunto.aElementos[i]);
                }
            }

            return resultado;
        }

        public void MostrarConjunto()
        {
            Console.Write("{ ");
            for (int i = 0; i < aNroElementos; i++)
            {
                Console.Write(aElementos[i] + (i < aNroElementos - 1 ? ", " : ""));
            }
            Console.WriteLine(" }");
        }
    }
}
```
# 2. Desarrolle una aplicación para conjuntos, utilizando la estructura dinámica de listas

```C#
using AppConjuntoLista;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace AppConjuntoLista
{
    internal class Program
    {
        static void Main(string[] args)
        {
            int[] A = { 3, 6, 4, 1, 2 };
            CConjunto C1 = new CConjunto(A);
            int[] B = { 1, 2, 5, 7, 6 };
            CConjunto C2 = new CConjunto(B);
            
            Console.WriteLine("Arreglo A ");
            C1.MostrarConjunto();
            Console.WriteLine("Arreglo B ");
            C2.MostrarConjunto();
            
            CConjunto union = C1.Union(C2);
            Console.WriteLine("Arreglo unión ");
            union.MostrarConjunto();

            CConjunto interseccion = C1.Interseccion(C2);
            Console.WriteLine("Arreglo intersección ");
            interseccion.MostrarConjunto();

            CConjunto diferencia = C1.Diferencia(C2);
            Console.WriteLine("Arreglo diferencia (A - B) ");
            diferencia.MostrarConjunto();

            CConjunto diferenciaSimetrica = C1.DiferenciaSimetrica(C2);
            Console.WriteLine("Arreglo diferencia simétrica ");
            diferenciaSimetrica.MostrarConjunto();

            Console.ReadKey();
        }
    }

    internal class CConjunto
    {
        // Atributos
        private List<int> aElementos;

        // Constructores
        public CConjunto()
        {
            aElementos = new List<int>();
        }

        public CConjunto(int[] pElementos)
        {
            aElementos = new List<int>();
            for (int i = 0; i < pElementos.Length; i++)
            {
                if (!aElementos.Contains(pElementos[i]))
                {
                    aElementos.Add(pElementos[i]);
                }
            }
        }

        // Modificadores
        public void ModificarElementos(int[] pElementos)
        {
            aElementos.Clear();
            for (int i = 0; i < pElementos.Length; i++)
            {
                if (!aElementos.Contains(pElementos[i]))
                {
                    aElementos.Add(pElementos[i]);
                }
            }
        }

        public void ModificarElemento(int pElemento, int pPosicion)
        {
            if (0 <= pPosicion && pPosicion < aElementos.Count)
            {
                aElementos[pPosicion] = pElemento;
            }
        }

        // Selectores
        public List<int> SeleccionarElementos()
        {
            return aElementos;
        }

        public int SeleccionarElemento(int pPosicion)
        {
            return aElementos[pPosicion];
        }

        // Otros métodos
        private int BusquedaSecuencial(CConjunto A, int X)
        {
            for (int i = 0; i < A.aElementos.Count; i++)
            {
                if (X == A.aElementos[i])
                {
                    return i;
                }
            }
            return -1;
        }

        public CConjunto Union(CConjunto A)
        {
            CConjunto resultado = new CConjunto();
            foreach (int elemento in aElementos)
            {
                resultado.Agregar(elemento);
            }

            foreach (int elemento in A.aElementos)
            {
                if (!resultado.aElementos.Contains(elemento))
                {
                    resultado.Agregar(elemento);
                }
            }

            return resultado;
        }

        public CConjunto Interseccion(CConjunto A)
        {
            CConjunto resultado = new CConjunto();
            foreach (int elemento in aElementos)
            {
                if (A.aElementos.Contains(elemento))
                {
                    resultado.Agregar(elemento);
                }
            }
            return resultado;
        }

        public CConjunto Diferencia(CConjunto A)
        {
            CConjunto resultado = new CConjunto();
            foreach (int elemento in aElementos)
            {
                if (!A.aElementos.Contains(elemento))
                {
                    resultado.Agregar(elemento);
                }
            }
            return resultado;
        }

        public CConjunto DiferenciaSimetrica(CConjunto A)
        {
            CConjunto resultado = new CConjunto();
            foreach (int elemento in aElementos)
            {
                if (!A.aElementos.Contains(elemento))
                {
                    resultado.Agregar(elemento);
                }
            }

            foreach (int elemento in A.aElementos)
            {
                if (!aElementos.Contains(elemento))
                {
                    resultado.Agregar(elemento);
                }
            }

            return resultado;
        }

        // Mostrar conjunto
        public void MostrarConjunto()
        {
            Console.Write("{ ");
            for (int i = 0; i < aElementos.Count; i++)
            {
                Console.Write(aElementos[i] + (i < aElementos.Count - 1 ? ", " : ""));
            }
            Console.WriteLine(" }");
        }

        // Método auxiliar para agregar elementos sin duplicados
        private void Agregar(int elemento)
        {
            if (!aElementos.Contains(elemento))
            {
                aElementos.Add(elemento);
            }
        }
    }
}
```
#  3 Desarrolle la aplicación para polinomios, utilizando arreglos estáticos
- # vision del conseptor 
- Clase `CPolinomio`:
- ## Atributos:
 - `aCoeficientes`: Arreglo de enteros que almacena los coeficientes de cada término del polinomio.
 - `aExponentes`: Arreglo de enteros que almacena los exponentes correspondientes a cada coeficiente.
- `aTerminos`: Entero que indica el número de términos en el polinomio.
- ## Constructores:
- `CPolinomio(int[] coeficientes, int[] exponentes)`: Inicializa el polinomio con los coeficientes y exponentes proporcionados.
- ## Métodos :
- `Sumar(CPolinomio otro)`: Suma dos polinomios y devuelve el polinomio resultante.
- `Restar(CPolinomio otro)`: Resta dos polinomios y devuelve el polinomio resultante.
- `Multiplicar(CPolinomio otro)`: Multiplica dos polinomios y devuelve el polinomio resultante.
- ## Mostrar Polinomio:
- `MostrarPolinomio()`: Muestra el polinomio en un formato legible (ejemplo: `3x^2 + 4x^1 + 2`).
```C#
using System;

namespace AppPolinomio
{
    internal class Program
    {
        static void Main(string[] args)
        {
            // Polinomios de ejemplo
            int[] coeficientesA = { 3, 4, 2 }; // Coeficientes del polinomio A
            int[] exponentesA = { 2, 1, 0 };   // Exponentes del polinomio A
            CPolinomio P1 = new CPolinomio(coeficientesA, exponentesA);

            int[] coeficientesB = { 5, -1, 1 }; // Coeficientes del polinomio B
            int[] exponentesB = { 3, 1, 0 };    // Exponentes del polinomio B
            CPolinomio P2 = new CPolinomio(coeficientesB, exponentesB);

            Console.WriteLine("Polinomio A:");
            P1.MostrarPolinomio();
            Console.WriteLine("Polinomio B:");
            P2.MostrarPolinomio();

            // Suma de Polinomios
            CPolinomio suma = P1.Sumar(P2);
            Console.WriteLine("Suma de A y B:");
            suma.MostrarPolinomio();

            // Resta de Polinomios
            CPolinomio resta = P1.Restar(P2);
            Console.WriteLine("Resta de A y B (A - B):");
            resta.MostrarPolinomio();

            // Multiplicación de Polinomios
            CPolinomio multiplicacion = P1.Multiplicar(P2);
            Console.WriteLine("Multiplicación de A y B:");
            multiplicacion.MostrarPolinomio();

            Console.ReadKey();
        }
    }

    internal class CPolinomio
    {
        // Atributos
        private int[] aCoeficientes;
        private int[] aExponentes;
        private int aTerminos; // Número de términos en el polinomio

        // Constructor
        public CPolinomio(int[] coeficientes, int[] exponentes)
        {
            aTerminos = coeficientes.Length;
            aCoeficientes = new int[aTerminos];
            aExponentes = new int[aTerminos];

            for (int i = 0; i < aTerminos; i++)
            {
                aCoeficientes[i] = coeficientes[i];
                aExponentes[i] = exponentes[i];
            }
        }

        // Métodos para operar polinomios
        public CPolinomio Sumar(CPolinomio otro)
        {
            int[] coefSum = new int[aTerminos + otro.aTerminos];
            int[] expSum = new int[aTerminos + otro.aTerminos];
            int indice = 0;

            // Añadir términos de este polinomio
            for (int i = 0; i < aTerminos; i++)
            {
                coefSum[indice] = aCoeficientes[i];
                expSum[indice] = aExponentes[i];
                indice++;
            }

            // Añadir términos del otro polinomio
            for (int i = 0; i < otro.aTerminos; i++)
            {
                bool encontrado = false;
                for (int j = 0; j < indice; j++)
                {
                    if (expSum[j] == otro.aExponentes[i])
                    {
                        coefSum[j] += otro.aCoeficientes[i];
                        encontrado = true;
                        break;
                    }
                }
                if (!encontrado)
                {
                    coefSum[indice] = otro.aCoeficientes[i];
                    expSum[indice] = otro.aExponentes[i];
                    indice++;
                }
            }

            // Crear el polinomio resultante
            return new CPolinomio(FiltrarCeros(coefSum, indice), FiltrarCeros(expSum, indice));
        }

        public CPolinomio Restar(CPolinomio otro)
        {
            int[] coefRest = new int[otro.aTerminos];
            for (int i = 0; i < otro.aTerminos; i++)
            {
                coefRest[i] = -otro.aCoeficientes[i];
            }

            CPolinomio polinomioNegativo = new CPolinomio(coefRest, otro.aExponentes);
            return Sumar(polinomioNegativo);
        }

        public CPolinomio Multiplicar(CPolinomio otro)
        {
            int[] coefMult = new int[aTerminos * otro.aTerminos];
            int[] expMult = new int[aTerminos * otro.aTerminos];
            int indice = 0;

            for (int i = 0; i < aTerminos; i++)
            {
                for (int j = 0; j < otro.aTerminos; j++)
                {
                    coefMult[indice] = aCoeficientes[i] * otro.aCoeficientes[j];
                    expMult[indice] = aExponentes[i] + otro.aExponentes[j];
                    indice++;
                }
            }

            // Crear el polinomio resultante
            return new CPolinomio(FiltrarCeros(coefMult, indice), FiltrarCeros(expMult, indice));
        }

        // Mostrar el polinomio
        public void MostrarPolinomio()
        {
            for (int i = 0; i < aTerminos; i++)
            {
                Console.Write($"{aCoeficientes[i]}x^{aExponentes[i]} ");
                if (i < aTerminos - 1) Console.Write("+ ");
            }
            Console.WriteLine();
        }

        // Método auxiliar para eliminar términos con coeficiente 0
        private int[] FiltrarCeros(int[] arreglo, int longitud)
        {
            int count = 0;
            for (int i = 0; i < longitud; i++)
            {
                if (arreglo[i] != 0) count++;
            }

            int[] resultado = new int[count];
            int index = 0;
            for (int i = 0; i < longitud; i++)
            {
                if (arreglo[i] != 0)
                {
                    resultado[index] = arreglo[i];
                    index++;
                }
            }

            return resultado;
        }
    }
}

```
# 4 Desarrolle la aplicación para polinomios, utilizando listas
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace AppPolinomioLista
{
    internal class Program
    {
        static void Main(string[] args)
        {
            List<int> coeficientesA = new List<int> { 3, 4, 2 }; // Coeficientes del polinomio A
            List<int> exponentesA = new List<int> { 2, 1, 0 };   // Exponentes del polinomio A
            CPolinomio P1 = new CPolinomio(coeficientesA, exponentesA);

            List<int> coeficientesB = new List<int> { 5, -1, 1 }; // Coeficientes del polinomio B
            List<int> exponentesB = new List<int> { 3, 1, 0 };    // Exponentes del polinomio B
            CPolinomio P2 = new CPolinomio(coeficientesB, exponentesB);

            Console.WriteLine("Polinomio A:");
            P1.MostrarPolinomio();
            Console.WriteLine("Polinomio B:");
            P2.MostrarPolinomio();

            CPolinomio suma = P1.Sumar(P2);
            Console.WriteLine("Suma de A y B:");
            suma.MostrarPolinomio();

            CPolinomio resta = P1.Restar(P2);
            Console.WriteLine("Resta de A y B (A - B):");
            resta.MostrarPolinomio();

            CPolinomio multiplicacion = P1.Multiplicar(P2);
            Console.WriteLine("Multiplicación de A y B:");
            multiplicacion.MostrarPolinomio();

            Console.ReadKey();
        }
    }

    internal class CPolinomio
    {
        // Atributos
        private List<int> aCoeficientes;
        private List<int> aExponentes;

        // Constructores
        public CPolinomio()
        {
            aCoeficientes = new List<int>();
            aExponentes = new List<int>();
        }

        public CPolinomio(List<int> coeficientes, List<int> exponentes)
        {
            aCoeficientes = new List<int>(coeficientes);
            aExponentes = new List<int>(exponentes);
        }

        // Modificadores
        public void ModificarTermino(int coeficiente, int exponente)
        {
            int indice = aExponentes.IndexOf(exponente);
            if (indice != -1)
            {
                aCoeficientes[indice] = coeficiente;
            }
            else
            {
                aCoeficientes.Add(coeficiente);
                aExponentes.Add(exponente);
            }
        }

        // Métodos
        public CPolinomio Sumar(CPolinomio otro)
        {
            CPolinomio resultado = new CPolinomio(aCoeficientes, aExponentes);

            for (int i = 0; i < otro.aCoeficientes.Count; i++)
            {
                resultado.ModificarTermino(otro.aCoeficientes[i], otro.aExponentes[i]);
            }

            return resultado;
        }

        public CPolinomio Restar(CPolinomio otro)
        {
            CPolinomio resultado = new CPolinomio(aCoeficientes, aExponentes);

            for (int i = 0; i < otro.aCoeficientes.Count; i++)
            {
                resultado.ModificarTermino(-otro.aCoeficientes[i], otro.aExponentes[i]);
            }

            return resultado;
        }

        public CPolinomio Multiplicar(CPolinomio otro)
        {
            CPolinomio resultado = new CPolinomio();

            for (int i = 0; i < aCoeficientes.Count; i++)
            {
                for (int j = 0; j < otro.aCoeficientes.Count; j++)
                {
                    int nuevoCoef = aCoeficientes[i] * otro.aCoeficientes[j];
                    int nuevoExp = aExponentes[i] + otro.aExponentes[j];

                    int indice = resultado.aExponentes.IndexOf(nuevoExp);
                    if (indice != -1)
                    {
                        resultado.aCoeficientes[indice] += nuevoCoef;
                    }
                    else
                    {
                        resultado.aCoeficientes.Add(nuevoCoef);
                        resultado.aExponentes.Add(nuevoExp);
                    }
                }
            }

            return resultado;
        }

        // Mostrar polinomio
        public void MostrarPolinomio()
        {
            for (int i = 0; i < aCoeficientes.Count; i++)
            {
                Console.Write($"{aCoeficientes[i]}x^{aExponentes[i]}");
                if (i < aCoeficientes.Count - 1) Console.Write(" + ");
            }
            Console.WriteLine();
        }
    }
}

```
# 5. Implemente la aplicación de polimorfismo utilizando listas y extienda para el tratamiento de trabajadores administrativos. Su aplicación debe permitir contar si hay más alumnos, docentes o trabajadores administrativos registrados en la lista.
- # Program.cs
```C#
using System;
using System.Collections.Generic;
using System.Linq;

namespace AppHerencia
{
    internal class Program
    {
        public class AppPolimorfismo03
        {
            /********************** Módulos genéricos *****************/
            public static String texto()
            {
                return Console.ReadLine();
            }

            public static int entero()
            {
                return Int32.Parse(texto());
            }

            public static void escribir(Object objeto)
            {
                Console.Write(objeto);
            }

            public static void escribirLn(Object objeto)
            {
                Console.WriteLine(objeto);
            }

            /*************** Módulos de la aplicación ***************/
            public static void menu()
            {
                escribirLn("");
                escribirLn("Menú de Lista de Personas");
                escribirLn("==========================");
                escribirLn("");
                escribirLn("1.- Ingresar Alumno");
                escribirLn("2.- Ingresar Docente");
                escribirLn("3.- Ingresar Trabajador Administrativo");
                escribirLn("4.- Mostrar datos de un Alumno o Docente");
                escribirLn("5.- Listar Alumnos");
                escribirLn("6.- Listar Docentes");
                escribirLn("7.- Listar Trabajadores Administrativos");
                escribirLn("8.- Contar tipos de personas");
                escribirLn("9.- Salir");
            }

            public static void ingresarAlumno(List<CPersona> lista)
            {
                escribirLn("");
                escribirLn("Ingrese datos de un Alumno: ");
                escribirLn("============================");
                escribirLn("");
                escribir("Nombres  : ");
                String nombres = texto();
                escribir("DNI      : ");
                String DNI = texto();
                escribir("Codigo   : ");
                String Codigo = texto();
                escribir("Carrera  : ");
                String Carrera = texto();
                CAlumno alumno = new CAlumno(nombres, DNI, Codigo, Carrera);
                lista.Add(alumno);
            }

            public static void ingresarDocente(List<CPersona> lista)
            {
                escribirLn("");
                escribirLn("Ingrese datos de un Docente:");
                escribirLn("============================");
                escribirLn("");
                escribir("Nombres        : ");
                String nombres = texto();
                escribir("DNI            : ");
                String dni = texto();
                escribir("Codigo         : ");
                String codigo = texto();
                escribir("Dpto. Académico: ");
                String dptoAcademico = texto();
                CDocente docente = new CDocente(nombres, dni, codigo, dptoAcademico);
                lista.Add(docente);
            }

            public static void ingresarTrabajadorAdministrativo(List<CPersona> lista)
            {
                escribirLn("");
                escribirLn("Ingrese datos de un Trabajador Administrativo:");
                escribirLn("==============================================");
                escribirLn("");
                escribir("Nombres        : ");
                String nombres = texto();
                escribir("DNI            : ");
                String dni = texto();
                escribir("Código         : ");
                String codigo = texto();
                escribir("Área           : ");
                String area = texto();
                CTrabajadorAdministrativo trabajador = new CTrabajadorAdministrativo(nombres, dni, codigo, area);
                lista.Add(trabajador);
            }

            public static void mostrarDatosAlumnoDocente(List<CPersona> lista)
            {
                escribirLn("");
                escribir("Ingrese un DNI de Alumno o Docente:");
                String dni = texto();
                CPersona persona = lista.OfType<CPersona>().FirstOrDefault(p => p.DNI().Equals(dni));

                if (persona != null)
                {
                    persona.mostrar();
                }
                else
                {
                    escribirLn("DNI no existe en la lista");
                }
            }

            public static void listarAlumnos(int n, List<CPersona> lista)
            {
                if (n > 0)
                {
                    listarAlumnos(n - 1, lista);
                    if (lista.ElementAt(n - 1) is CAlumno alumno)
                    {
                        alumno.mostrar();
                    }
                }
            }

            public static void listarDocentes(int n, List<CPersona> lista)
            {
                if (n > 0)
                {
                    listarDocentes(n - 1, lista);
                    if (lista.ElementAt(n - 1) is CDocente docente)
                    {
                        docente.mostrar();
                    }
                }
            }

            public static void listarTrabajadoresAdministrativos(int n, List<CPersona> lista)
            {
                if (n > 0)
                {
                    listarTrabajadoresAdministrativos(n - 1, lista);
                    if (lista.ElementAt(n - 1) is CTrabajadorAdministrativo trabajador)
                    {
                        trabajador.mostrar();
                    }
                }
            }

            public static void contarTipos(List<CPersona> lista)
            {
                int alumnos = lista.Count(p => p is CAlumno);
                int docentes = lista.Count(p => p is CDocente);
                int trabajadores = lista.Count(p => p is CTrabajadorAdministrativo);

                escribirLn("");
                escribirLn("Conteo de personas registradas:");
                escribirLn($"Alumnos: {alumnos}");
                escribirLn($"Docentes: {docentes}");
                escribirLn($"Trabajadores Administrativos: {trabajadores}");
            }

            /* --------------- Main ------------------ */
            static void Main(string[] args)
            {
                List<CPersona> lista = new List<CPersona>();
                int opcion;
                do
                {
                    menu();
                    escribir("Ingresa Opcion: ");
                    opcion = entero();
                    switch (opcion)
                    {
                        case 1:
                            ingresarAlumno(lista);
                            break;
                        case 2:
                            ingresarDocente(lista);
                            break;
                        case 3:
                            ingresarTrabajadorAdministrativo(lista);
                            break;
                        case 4:
                            mostrarDatosAlumnoDocente(lista);
                            break;
                        case 5:
                            escribir("");
                            escribir("Listado de Alumnos");
                            listarAlumnos(lista.Count, lista);
                            break;
                        case 6:
                            escribir("");
                            escribir("Listado de Docentes");
                            listarDocentes(lista.Count, lista);
                            break;
                        case 7:
                            escribir("");
                            escribir("Listado de Trabajadores Administrativos");
                            listarTrabajadoresAdministrativos(lista.Count, lista);
                            break;
                        case 8:
                            contarTipos(lista);
                            break;
                    }
                } while (opcion < 9);
            }
        }
    }
}

```
- # CPersona
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace AppHerencia
{
    internal class CPersona
    {
        /* ******************* ATRIBUTOS ******************* */
        protected string aNombres;
        protected string aDNI;
        /* ******************* METODOS ********************* */
        /* ================= Constructores ================= */
        /* -------------------------------------------------*/
        public CPersona()
        {
            aNombres = "";
            aDNI = "";
        }
        /* -------------------------------------------------*/
        public CPersona(string pNombres, string pDNI)
        {
            aNombres = pNombres;
            aDNI = pDNI;
        }
        /* ================= Modificadores ================= */
        /* -------------------------------------------------*/
        public void modificarNombres(string pNombres)
        {
            aNombres = pNombres;
        }
        /* -------------------------------------------------*/
        public void modificarDNI(string pDNI)
        {
            aDNI = pDNI;
        }
        /* =================   Selectores  ================= */
        public string nombres()
        {
            return aNombres;
        }
        /* -------------------------------------------------*/
        public string DNI()
        {
            return aDNI;
        }
        /* *************** Otros Metodos ****************** */
        public override string ToString()
        {
            return aNombres + " " + aDNI;
        }
        /* -------------------------------------------------*/
        public override bool Equals(Object objeto)
        {
            return ToString().Equals(objeto.ToString());
        }
        /* -------------------------------------------------*/
        public virtual void mostrar()
        {
            Console.WriteLine();
            Console.WriteLine("Datos de Persona");
            Console.WriteLine("================");
            Console.WriteLine("Nombres : " + aNombres);
            Console.WriteLine("DNI     : " + aDNI);
        }
    }
}
```
- # CAlumno.cs
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace AppHerencia
{
    internal class CAlumno : CPersona
    {
        /* ******************    ATRIBUTOS    ************** */
        private string aCodigo;
        private string aCarrera;
        /* ******************     METODOS     ************** */
        /* ================= Constructores ================= */
        public CAlumno() : base()
        {
            aCodigo = "";
            aCarrera = "";
        }
        /* -------------------------------------------------*/
        public CAlumno(string pNombres, string pDNI, string pCodigo, string pCarrera) : base(pNombres, pDNI)
        {
            aCodigo = pCodigo;
            aCarrera = pCarrera;
        }
        /* ================= Modificadores ================= */
        public void modificarCodigo(string pCodigo)
        {
            aCodigo = pCodigo;
        }
        /* -------------------------------------------------*/
        public void modificarCarrera(string pCarrera)
        {
            aCarrera = pCarrera;
        }
        /* =================  Selectores  ================== */
        public string codigo()
        {
            return aCodigo;
        }
        /* -------------------------------------------------*/
        public string carrera()
        {
            return aCarrera;
        }
        /* ================  Otros Metodos  ================ */
        public new string ToString()
        {
            return aNombres + " " + aDNI + " - " + aCodigo + " + " + aCarrera;
        }
        /* -------------------------------------------------*/
        public new bool Equals(Object pCodigo)
        {
            return aCodigo.Equals(pCodigo.ToString());
        }
        /* -------------------------------------------------*/
        public override void mostrar()
        {
            Console.WriteLine();
            Console.WriteLine("Datos de Alumno");
            Console.WriteLine("================");
            Console.WriteLine("Nombres   : " + aNombres);
            Console.WriteLine("Dirección : " + aDNI);
            Console.WriteLine("Código    : " + aCodigo);
            Console.WriteLine("Carrera   : " + aCarrera);
        }
    }
}
```
- # CDocente.cs
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace AppHerencia
{
    internal class CDocente : CPersona
    {
        /* ******************    ATRIBUTOS    ************** */
        private string aCodigo;
        private string aDepartamento;
        /* ******************     METODOS     ************** */
        /* ================= Constructores ================= */
        public CDocente() : base()
        {
            aCodigo = "";
            aDepartamento = "";
        }
        /* -------------------------------------------------*/
        public CDocente(string pNombres, string pDNI, string pCodigo, string pDepartamento) : base(pNombres, pDNI)
        {
            aCodigo = pCodigo;
            aDepartamento = pDepartamento;
        }
        /* ================= Modificadores ================= */
        public void modificarCodigo(string pCodigo)
        {
            aCodigo = pCodigo;
        }
        /* -------------------------------------------------*/
        public void modificarDepartamento(string pDepartamento)
        {
            aDepartamento = pDepartamento;
        }
        /* selectores  ================== */
        public string codigo()
        {
            return aCodigo;
        }
        /* -------------------------------------------------*/
        public string departamento()
        {
            return aDepartamento;
        }
        /* ================  Otros Metodos  ================ */
        public new string ToString()
        {
            return aNombres + " - " + aDNI + " - " + aCodigo + " - " + aDepartamento;
        }
        /* -------------------------------------------------*/
        public new bool Equals(Object pCodigo)
        {
            return aCodigo.Equals(pCodigo.ToString());
        }
        /* -------------------------------------------------*/
        public override void mostrar()
        {
            Console.WriteLine();
            Console.WriteLine("Datos del DOCENTE");
            Console.WriteLine("==================");
            Console.WriteLine("Nombres   : " + aNombres);
            Console.WriteLine("Dirección : " + aDNI);
            Console.WriteLine("Código    : " + aCodigo);
            Console.WriteLine("Carrera   : " + aDepartamento);
        }
    }
}
```
- # CTrabajadorAdministrativo.cs
```C#
using System;

namespace AppHerencia
{
    internal class CTrabajadorAdministrativo : CPersona
    {
        /* ******************    ATRIBUTOS    ************** */
        private string aCodigo;
        private string aArea;
        /* ******************     METODOS     ************** */
        /* ================= Constructores ================= */
        public CTrabajadorAdministrativo() : base()
        {
            aCodigo = "";
            aArea = "";
        }
        /* -------------------------------------------------*/
        public CTrabajadorAdministrativo(string pNombres, string pDNI, string pCodigo, string pArea) : base(pNombres, pDNI)
        {
            aCodigo = pCodigo;
            aArea = pArea;
        }
        /* ================= Modificadores ================= */
        public void modificarCodigo(string pCodigo)
        {
            aCodigo = pCodigo;
        }
        /* -------------------------------------------------*/
        public void modificarArea(string pArea)
        {
            aArea = pArea;
        }
        /* ==================   Selectores   ================== */
        public string codigo()
        {
            return aCodigo;
        }
        /* -------------------------------------------------*/
        public string area()
        {
            return aArea;
        }
        /* ================  Otros Métodos  ================ */
        public override string ToString()
        {
            return $"{aNombres} - {aDNI} - {aCodigo} - {aArea}";
        }
        public override void mostrar()
        {
            Console.WriteLine();
            Console.WriteLine("Datos del TRABAJADOR ADMINISTRATIVO");
            Console.WriteLine("==================");
            Console.WriteLine("Nombres   : " + aNombres);
            Console.WriteLine("DNI       : " + aDNI);
            Console.WriteLine("Código    : " + aCodigo);
            Console.WriteLine("Área      : " + aArea);
        }
    }
}

```
