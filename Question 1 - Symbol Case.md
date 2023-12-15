Lower case symbols are not accepted. E.g. if you enter 'q' it is not recognised as 'Q'. Fix this.

```csharp
private string GetSymbolFromUser()
{
     string Symbol = "";
     while (!AllowedSymbols.Contains(Symbol))
     {
          Console.Write("Enter symbol: ");
          Symbol = Console.ReadLine().ToUpper();
      }
      return Symbol;
}
```
