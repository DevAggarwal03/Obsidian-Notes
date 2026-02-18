Recursive Descent Parser: A type of Top Down Parser that starts from the start symbol 'S' of a Grammar and recursively checks if the productions match with the given input stream of tokes. 
- This parser cannot be made for Grammar containing: 
	- Left Recursion
	- Non - Deterministic Grammar (Left factoring is required)
- Here Each non-terminal of the grammar has a function that further derives the string, and returns when the production reach it's end