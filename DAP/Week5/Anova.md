**Anova uses F-statistic for calculation**

![[Pasted image 20260413195038.png]]

step1: calc SST -> total, SSB -> Between column, SSE -> Enherent
step2: calc Degrees of Freedom of diff sum of Square
- SST => 9 - 1 => 8
- SSB => 3 - 1 => 2
- SSE => 2 + 2 + 2 => 6
	- 1st column: 3 - 1
	- 2nd column: 3 - 1
	- 3rd column: 3 - 1
step3: Calculate MS (mean square) for Between and inherent: SS/df
step4: Divide MSB/MSE to get **F**(statistic value)
step5: see the position of F using the F-table to make you decision about the Hypothesis

![[Pasted image 20260413195806.png]]


[[python code for anova]]
[[GeneralAnova]]