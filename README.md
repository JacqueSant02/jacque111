using System;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        Console.Write("Quantos funcionários serão registrados? ");
        int n = int.Parse(Console.ReadLine());

        List<Funcionario> funcionarios = new List<Funcionario>();

        for (int i = 0; i < n; i++)
        {
            Console.WriteLine($"Func #{i + 1}:");
            Console.Write("Id: ");
            int id = int.Parse(Console.ReadLine());
            Console.Write("Nome: ");
            string nome = Console.ReadLine();
            Console.Write("Salário: ");
            double salario = double.Parse(Console.ReadLine());
            funcionarios.Add(new Funcionario(id, nome, salario));
        }

        Console.Write("Entre com o ID de quem receberá o reajuste: ");
        int idReajuste = int.Parse(Console.ReadLine());

        Funcionario funcionario = funcionarios.Find(x => x.Id == idReajuste);
        if (funcionario != null)
        {
            Console.Write("Entre com a porcentagem de aumento: ");
            double porcentagem = double.Parse(Console.ReadLine());
            funcionario.AumentarSalario(porcentagem);
        }
        else
        {
            Console.WriteLine("Este ID não existe");
        }

        Console.WriteLine("\nLista atualizada:");
        foreach (Funcionario obj in funcionarios)
        {
            Console.WriteLine(obj);
        }
    }
}

class Funcionario
{
    public int Id { get; set; }
    public string Nome { get; set; }
    private double salario;

    public Funcionario(int id, string nome, double salario)
    {
        Id = id;
        Nome = nome;
        this.salario = salario;
    }

    public void AumentarSalario(double porcentagem)
    {
        salario += salario * porcentagem / 100.0;
    }

    public override string ToString()
    {
        return Id + ", " + Nome + ", " + salario.ToString("F2");
    }
}
