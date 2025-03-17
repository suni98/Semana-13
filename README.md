# Semana-13
using System;
using System.Collections.Generic;

public class Revista
{
    public string Titulo { get; set; }

    public Revista(string titulo)
    {
        Titulo = titulo;
    }
}

public class CatalogoRevistas
{
    private List<Revista> revistas = new List<Revista>();

    public void AgregarRevista(Revista revista)
    {
        revistas.Add(revista);
    }

    // Búsqueda iterativa
    public bool BuscarTituloIterativo(string titulo)
    {
        foreach (var revista in revistas)
        {
            if (revista.Titulo.Equals(titulo, StringComparison.OrdinalIgnoreCase))
            {
                return true;
            }
        }
        return false;
    }

    // Búsqueda recursiva
    public bool BuscarTituloRecursivo(string titulo, int indice = 0)
    {
        if (indice >= revistas.Count)
        {
            return false;
        }

        if (revistas[indice].Titulo.Equals(titulo, StringComparison.OrdinalIgnoreCase))
        {
            return true;
        }

        return BuscarTituloRecursivo(titulo, indice + 1);
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        CatalogoRevistas catalogo = new CatalogoRevistas();

        // Agregar 10 títulos de revistas
        catalogo.AgregarRevista(new Revista("National Geographic"));
        catalogo.AgregarRevista(new Revista("Time"));
        catalogo.AgregarRevista(new Revista("Science"));
        catalogo.AgregarRevista(new Revista("Nature"));
        catalogo.AgregarRevista(new Revista("Forbes"));
        catalogo.AgregarRevista(new Revista("Vogue"));
        catalogo.AgregarRevista(new Revista("The Economist"));
        catalogo.AgregarRevista(new Revista("Sports Illustrated"));
        catalogo.AgregarRevista(new Revista("Wired"));
        catalogo.AgregarRevista(new Revista("Rolling Stone"));

        while (true)
        {
            Console.WriteLine("\n--- Menú ---");
            Console.WriteLine("1. Buscar título (iterativo)");
            Console.WriteLine("2. Buscar título (recursivo)");
            Console.WriteLine("3. Salir");
            Console.Write("Ingrese la opción: ");

            string opcion = Console.ReadLine();

            switch (opcion)
            {
                case "1":
                    BuscarTitulo(catalogo, true);
                    break;
                case "2":
                    BuscarTitulo(catalogo, false);
                    break;
                case "3":
                    return;
                default:
                    Console.WriteLine("Opción no válida.");
                    break;
            }
        }
    }

    public static void BuscarTitulo(CatalogoRevistas catalogo, bool iterativo)
    {
        Console.Write("Ingrese el título a buscar: ");
        string tituloBuscar = Console.ReadLine();

        bool encontrado = iterativo ? catalogo.BuscarTituloIterativo(tituloBuscar) : catalogo.BuscarTituloRecursivo(tituloBuscar);

        Console.WriteLine(encontrado ? "Encontrado" : "No encontrado");
    }
}
