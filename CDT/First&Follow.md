![[First and Follow rules.png]] 

First( A )  : all the terminals that occur in the first position of A's production.  
Follow( A ): gives the set of terminals that may come immediately to the right of A in any string satisfying the grammar

Follow( ):
	- Follow(start) = {$} (start symbols follow always has $)
	- Follow( ) = Cannot contain Epsilon
First( ):
	- First( ) = can contain epsilon