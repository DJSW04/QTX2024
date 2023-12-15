When you try place a symbol in a invalid cell it still counts as a placed cell towards the amount of symbols placed.

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
        //SymbolsLeft -= 1; => moved inside the IF statement
        Cell CurrentCell = GetCell(Row, Column);
        if (CurrentCell.CheckSymbolAllowed(Symbol))
        {
            SymbolsLeft -= 1; //moved inside if statement to fix error
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

    }
    Console.WriteLine();
    DisplayPuzzle();
    Console.WriteLine();
    return Score;
}
```