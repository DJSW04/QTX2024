Alter the **attemptPuzzle** subroutine such that the user is asked if they wish to undo their last move prior to the place in the loop where there is a check for **symbolsLeft** being equal to zero. Warn them that this will lose them 3 points.

If the player chooses to undo:

a.      revert the **grid** back to its original state

b.      ensure **symbolsLeft** has the correct value

c.      ensure **score** reverts to its original value minus the 3 point undo penalty

d. ensure any changes made to a cell’s **symbolsNotAllowed** list are undone as required
