Implement a special character * which is a wildcard. The wildcard can be used to represent any character so that multiple matches can be made with the same cell. Give the player 3 wildcards in random positions at the start of the game.

a) Alter the standard Puzzle constructor (not the load game one) to call ChangeSymbolInCell for 3 random cells, passing in * as the new symbol. Note that blocked cells cannot be changed to wildcard ones so you need to add code to ensure the randomly selected cell is not a blocked cell.

b) In class Cell alter the method. ChangeSymbolInCell such that wildcard cells will never have their symbol changed from * once set. In the same class, alter method CheckSymbolAllowed such that wildcard cells always return true.

c) Alter method MatchesPattern in class Pattern to allow correct operation for the new wildcard *

d) Test that a wildcard can successfully match within two different patterns