Offer 'game difficulty' setting to change level of game (with greater number of blocked cells = 'more difficult')
```csharp
public Puzzle(int Size, int StartSymbols)
{
    Score = 0;
    SymbolsLeft = StartSymbols;
    GridSize = Size;
    Grid = new List<Cell>();

    // new code for question 5

    int notBlockedChance;
    Console.WriteLine("Would you like the difficulty to be easy (E), medium(M), hard(H) or extremely hard (EH)?");
    string difficulty = Console.ReadLine();
    if (difficulty.ToUpper() == "EH")
    {
        notBlockedChance = 50; //these values are just an example and can be modified
    }
    else if (difficulty.ToUpper() == "H")
    {
        notBlockedChance = 60;
    }
    else if (difficulty.ToUpper() == "M")
    {
        notBlockedChance = 75;
    }
    else
    {
        notBlockedChance = 90;
    }

    for (var Count = 1; Count <= GridSize * GridSize; Count++)
    {
        Cell C;

        if (Rng.Next(1, 101) < notBlockedChance)
        //end of new code for question 5
        {
            C = new Cell();
        }
        else
        {
            C = new BlockedCell();
        }
        Grid.Add(C);
    }
    AllowedPatterns = new List<Pattern>();
    AllowedSymbols = new List<string>();
    Pattern QPattern = new Pattern("Q", "QQ**Q**QQ");
    AllowedPatterns.Add(QPattern);
    AllowedSymbols.Add("Q");
    Pattern XPattern = new Pattern("X", "X*X*X*X*X");
    AllowedPatterns.Add(XPattern);
    AllowedSymbols.Add("X");
    Pattern TPattern = new Pattern("T", "TTT**T**T");
    AllowedPatterns.Add(TPattern);
    AllowedSymbols.Add("T");

}
```