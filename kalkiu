internal class Program
{
    private static void Main(string[] args)
    {
        Console.WriteLine("Dzień dobry właśnie korzysztasz z programu do oblocznia logarytmów i ciagów, miłego użytku :-)");
        while (true)
        {
            Console.WriteLine("\nWybierz opcję:");
            Console.WriteLine("1. Oblicz logarytm");
            Console.WriteLine("2. Oblicz ciąg");
            Console.WriteLine("3. Zakończ program");
            int opcja;
            while (!int.TryParse(Console.ReadLine(), out opcja) || opcja < 1 || opcja > 3)
            {
                Console.WriteLine("Wybierz poprawną opcję (1-3)!");
            }
            switch (opcja)
            {
                case 1:
                    Console.WriteLine("1. Oblicz działanie z logarytmem");
                    Console.WriteLine("2. Znajdz x np. log_7(x)=2");
                    Console.WriteLine("3. Znajdz x np. log_x(4)=2");
                    int opcja2;
                    while (!int.TryParse(Console.ReadLine(), out opcja2) || opcja2 < 1 || opcja2 < 4)
                    switch (opcja2)
                        {
                            case 1:
                                ObliczLogarytm();
                                Environment.Exit(0);
                                break;
                            case 2:
                                ZnajdzX();
                                Environment.Exit(0);
                                break;
                            case 3:
                                ZnajdzX2();
                                Environment.Exit(0);
                                break;
                        }
                    break;
                case 2:
                    ObliczCiag();
                    break;
                case 3:
                    Environment.Exit(0);
                    break;
            }
        }
    }
    static void ObliczLogarytm()
    {
        Console.WriteLine("Wpisz działanie do wykonania:");
        string expression = Console.ReadLine();

        try
        {
            expression = expression.Replace(" ", "");
            double result = Evaluate(expression);
            Console.WriteLine("Wynik: " + result);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Błąd: " + ex.Message);
            Environment.Exit(0);
        }
    }
    static double Evaluate(string expression)
    {

        while (expression.Contains("log_"))
        {
            int startIndex = expression.IndexOf("log_");
            int endIndex = expression.IndexOf(")", startIndex);
            string logExpr = expression.Substring(startIndex + 4, endIndex - startIndex - 4);
            string[] parts = logExpr.Split('(');
            double baseValue = double.Parse(parts[0]);
            double argument = double.Parse(parts[1].Replace(".", ","));
            double result = Math.Log(argument, baseValue);
            expression = expression.Replace($"log_{logExpr})", result.ToString().Replace(",", "."));
        }


        while (expression.Contains("log("))
        {
            int startIndex = expression.IndexOf("log(");
            int endIndex = expression.IndexOf(")", startIndex);
            string logExpr = expression.Substring(startIndex + 4, endIndex - startIndex - 4);
            double argument = double.Parse(logExpr.Replace(".", ","));
            double result = Math.Log(argument);
            expression = expression.Replace($"log({logExpr})", result.ToString().Replace(",", "."));
        }

        return EvaluateMathExpression(expression);
    }

    static double EvaluateMathExpression(string expression)
    {
        expression = expression.Replace("log_", "Math.Log(");

        return Convert.ToDouble(new System.Data.DataTable().Compute(expression, ""));
    }
    static void ZnajdzX()
    {
        Console.WriteLine("Wpisz równanie logarytmiczne do rozwiązania (np. log_2(x)=3 lub log(x)=2):");
        string expression = Console.ReadLine();

        expression = expression.Replace(" ", "");
        expression = expression.ToLower();

        if (!expression.StartsWith("log_") && !expression.StartsWith("log(") || !expression.Contains("="))
        {
            Console.WriteLine("Błąd: Nieprawidłowy format równania logarytmicznego!");
            return;
        }

        double result;
        if (expression.StartsWith("log("))
        {
            if (double.TryParse(expression.Substring(expression.IndexOf("=") + 1), out result))
            {
                double x = Math.Pow(Math.E,result);
                Console.WriteLine($"Wartość x to: {x}");
            }
            else
            {
                Console.WriteLine("Błąd: Nieprawidłowa wartość liczby!");
            }
        }
        else
        {
            string baseString = expression.Substring(4, expression.IndexOf("(") - 4);
            double logBase;
            if (double.TryParse(baseString, out logBase) && double.TryParse(expression.Substring(expression.IndexOf("=") + 1), out result))
            {
                double x = Math.Pow(logBase, result);
                Console.WriteLine($"Wartość x to: {x}");
            }
            else
            {
                Console.WriteLine("Błąd: Nieprawidłowa wartość podstawy logarytmu!");
            }
        }
    }
    static void ZnajdzX2()
    {
        Console.WriteLine("Wpisz równanie logarytmiczne do rozwiązania (np. log_x(4)=2):");
        string expression = Console.ReadLine();
        expression = expression.Replace(" ", "");
        if (!expression.StartsWith("log_") || !expression.Contains(")") || !expression.Contains("="))
        {
            Console.WriteLine("Błąd: Nieprawidłowy format równania!");
            return;
        }
        int baseIndex = expression.IndexOf("log_") + 4;
        int openParenIndex = expression.IndexOf("(");
        int closeParenIndex = expression.IndexOf(")");
        int equalIndex = expression.IndexOf("=");
        if (double.TryParse(expression.Substring(openParenIndex + 1, closeParenIndex - openParenIndex - 1), out double argument) &&
            double.TryParse(expression.Substring(equalIndex + 1), out double result))
        {
            double baseValue = Math.Pow(argument, 1 / result);
            Console.WriteLine($"Wartość podstawy logarytmu x to: {baseValue}");
        }
        else
        {
            Console.WriteLine("Błąd: Wprowadzono nieprawidłowe wartości!");
        }
    }
    static void ObliczCiag()
    {
        Console.WriteLine("Podaj długość ciągu:");
        int n = int.Parse(Console.ReadLine());
        double[] elements = new double[n];
        for (int i = 0; i < n; i++)
        {
            Console.WriteLine($"Podaj {i + 1} element ciągu:");
            elements[i] = double.Parse(Console.ReadLine());
        }
        double[] differences = new double[n - 1];
        for (int i = 0; i < n - 1; i++)
        {
            differences[i] = elements[i + 1] - elements[i];
        }
        bool isArithmetic = true;
        bool isGeometric = true;
        for (int i = 1; i < n - 1; i++)
        {
            if (differences[i] != differences[i - 1])
            {
                isArithmetic = false;
                break;
            }
        }
        double ratio = elements[1] / elements[0];
        for (int i = 1; i < n - 1; i++)
        {
            if (elements[i + 1] / elements[i] != ratio)
            {
                isGeometric = false;
                break;
            }
        }
        int czyrosnie=0;
        int sprawdzacz = 0;
        for (int i = 0; i< n-1; i++)
        {
            if (elements[i + 1] > elements[i])
            {
                czyrosnie = 1;
                if(sprawdzacz == 2)
                {
                    Console.WriteLine("Ciąg jest zmienny");
                    czyrosnie = 0;
                    break;
                }
                sprawdzacz = 1;  
            }else if (elements[i+1] < elements[i])
            {
                czyrosnie = 2;
                if(sprawdzacz == 1)
                {
                    Console.WriteLine("Ciąg jest zmienny");
                    czyrosnie = 0;
                    break;
                }
                sprawdzacz=2;
            }
            else
            {
                Console.WriteLine("Ciag jest stały");
                break;
            }
        }
        if(czyrosnie == 1)
        {
            Console.WriteLine("Ciag rośnie");
        }else if(czyrosnie == 2)
        {
            Console.WriteLine("Ciąg Maleje");
        }
        if (isArithmetic)
        {
            Console.WriteLine("Ciąg arytmetyczny");
        }
        else if (isGeometric)
        {
            Console.WriteLine("Ciąg geometryczny");
        }
        else
        {
            Console.WriteLine("Inny ciąg");
        }
        Console.WriteLine("Podaj wartość n:");
        int nth = int.Parse(Console.ReadLine());
        if (isArithmetic)
        {
            double a = elements[0];
            double d = differences[0];
            double nthElement = a + (nth - 1) * d;
            Console.WriteLine($"Wartość {nth} elementu ciągu wynosi: {nthElement}");
        }
        else if (isGeometric)
        {
            double a = elements[0];
            double r = ratio;
            double nthElement = a * Math.Pow(r, nth - 1);
            Console.WriteLine($"Wartość {nth} elementu ciągu wynosi: {nthElement}");
        }
        else
        {
            Console.WriteLine("Nie można obliczyć wartości elementu ciągu dla innego typu ciągu.");
        }
    }
}
