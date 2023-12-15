If a filename is entered that does not exist, the game is unplayable (infinite loop). Amend the program so that in this case the default game is played, with a suitable message to indicate this.

```csharp
static void Main(string[] args)
{
    string Again = "y";
    int Score;
    while (Again == "y")
    {
        Console.Write("Press Enter to start a standard puzzle or enter name of file to load: ");
        string Filename = Console.ReadLine();
        Puzzle MyPuzzle;
        if (Filename.Length > 0)
        {
            // new code for question 2 - use try/catch in main and otherwise cause default game to be played

            try
            {
                MyPuzzle = new Puzzle(Filename + ".txt");
            }
            catch
            {
                Console.WriteLine("Invalid file. Playing default puzzle instead.");
                MyPuzzle = new Puzzle(8, Convert.ToInt32(8 * 8 * 0.6));
            }
            // end of new code for question 2
        }
        else
        {
            MyPuzzle = new Puzzle(8, Convert.ToInt32(8 * 8 * 0.6));
        }
        Score = MyPuzzle.AttemptPuzzle();
        Console.WriteLine("Puzzle finished. Your score was: " + Score);
        Console.Write("Do another puzzle? ");
        Again = Console.ReadLine().ToLower();
    }
    Console.ReadLine();
}

// try/catch removed from loadPuzzle subroutine
private void LoadPuzzle(string Filename)
{

    using (StreamReader MyStream = new StreamReader(Filename))
    {
        int NoOfSymbols = Convert.ToInt32(MyStream.ReadLine());
        for (var Count = 1; Count <= NoOfSymbols; Count++)
        {
            AllowedSymbols.Add(MyStream.ReadLine());
        }
        int NoOfPatterns = Convert.ToInt32(MyStream.ReadLine());
        for (var Count = 1; Count <= NoOfPatterns; Count++)
        {
            List<string> Items = MyStream.ReadLine().Split(',').ToList();
            Pattern P = new Pattern(Items[0], Items[1]);
            AllowedPatterns.Add(P);
        }
        GridSize = Convert.ToInt32(MyStream.ReadLine());
        for (var Count = 1; Count <= GridSize * GridSize; Count++)
        {
            Cell C;
            List<string> Items = MyStream.ReadLine().Split(',').ToList();
            if (Items[0] == "@")
            {
                C = new BlockedCell();
            }
            else
            {
                C = new Cell();
                C.ChangeSymbolInCell(Items[0]);
                for (var CurrentSymbol = 1; CurrentSymbol < Items.Count; CurrentSymbol++)
                {
                    C.AddToNotAllowedSymbols(Items[CurrentSymbol]);
                }
            }
            Grid.Add(C);
        }
        Score = Convert.ToInt32(MyStream.ReadLine());
        SymbolsLeft = Convert.ToInt32(MyStream.ReadLine());
    }
}

}}
```
