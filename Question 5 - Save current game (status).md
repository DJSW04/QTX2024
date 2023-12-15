Save the current status of the game (file-handling)/writing to a text file.
```csharp
public virtual int AttemptPuzzle()
{
    bool Finished = false;
    while (!Finished)
    {
        DisplayPuzzle();
        Console.WriteLine("Current score: " + Score);
        bool Valid = false;
        int Row = -1;
        while (!Valid)
        {
            Console.Write("Enter row number: ");
            try
            {
                Row = Convert.ToInt32(Console.ReadLine());
                Valid = true;
            }
            catch
            {
            }
        }
        int Column = -1;
        Valid = false;
        while (!Valid)
        {
            Console.Write("Enter column number: ");
            try
            {
                Column = Convert.ToInt32(Console.ReadLine());
                Valid = true;
            }
            catch
            {
            }
        }
        string Symbol = GetSymbolFromUser();
        SymbolsLeft -= 1
        Cell CurrentCell = GetCell(Row, Column);
        if (CurrentCell.CheckSymbolAllowed(Symbol))
        {
            SymbolsLeft -= 1;
            CurrentCell.ChangeSymbolInCell(Symbol);
            int AmountToAddToScore = CheckForMatchWithPattern(Row, Column);
            if (AmountToAddToScore > 0)
            {
                Score += AmountToAddToScore;
            }
        }
        if (SymbolsLeft == 0)
        {
            Finished = true;
        }
        //New code for question 5 including calling new SavePuzzle() method:
        Console.WriteLine("Do you wish to save your puzzle and exit? (Y for yes)");
        if (Console.ReadLine().ToUpper() == "Y")
        {
            Console.WriteLine("What would you like to save your puzzle as?");
            string file = Console.ReadLine();
            SavePuzzle(file);
            Console.WriteLine("Puzzle Successfully Saved.");
            break;
        }
        //end of code for question 5
    }
    Console.WriteLine();
    DisplayPuzzle();
    Console.WriteLine();
    return Score;

//new SavePuzzle() method:
private void SavePuzzle(string filename)
{
    filename = filename + ".txt";
    using (StreamWriter sw = new StreamWriter(filename))
    {
        sw.WriteLine(AllowedSymbols.Count);
        foreach (var symbol in AllowedSymbols)
        {
            sw.WriteLine(symbol);
        }
        sw.WriteLine(AllowedPatterns.Count);
        foreach (var pattern in AllowedPatterns)
        {
            sw.WriteLine(pattern.GetPatternSymbol() + "," + pattern.GetPatternSequence());
        }
        sw.WriteLine(GridSize);

        foreach (Cell C in Grid)
        {
            List<string> notAllowedSymbol = C.returnNotAllowedSymbols();
            try
            {
                sw.WriteLine(C.GetSymbol() + "," + notAllowedSymbol[0]);
            }
            catch
            {
                sw.WriteLine(C.GetSymbol() + ",");
            }
        }
        sw.WriteLine(Score);
        sw.WriteLine(SymbolsLeft);
    }
}

// new returnNotAllowedSymbol() method in Pattern class 
public virtual List<string> returnNotAllowedSymbols()
{
    return SymbolsNotAllowed;
}
```