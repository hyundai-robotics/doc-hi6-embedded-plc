# 4.31 NEXT (NEXT): Next Block


### Description
The operation will be performed according to the "step" of the FOR instructions.
If the "step" value is greater than 0, the execution will occur repeatedly until the "idx" relay value becomes less than or equal to the "final" value.
If the "step" value is less than 0, the execution will occur repeatedly until the "idx" relay value becomes greater than or equal to the "final" value.
If a NEXT instruction is executed without a FOR instruction, the NEXT instruction will be ignored.
Caution:  
The FOR/NEXT instruction does not have any additional processing for branching. As such, if a FOR instruction is recorded inside a branch, and a NEXT instruction is recorded outside the branch or inside another branch, the FOR instructions will not operate correctly.
Note: For more details on the FOR instructions, refer to [4.30 FOR (FOR)](./30-for)

<br>

### Example of use

Refer to the example on the use of the FOR instructions.
