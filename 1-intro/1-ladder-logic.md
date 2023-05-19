# 1.1 Ladder logic

Ladder Logic, or Ladder Diagram (LD), is the main programming method for embedded PLCs. [Besides LD, there are other methods such as Structured Text (ST), Function Block Diagram (FBD), and Sequential Function Chart (SFC), but embedded PLCs do not support them and will not be further discussed.]

The reason the ladder program is so named is that the architecture of the program resembles a ladder. The horizontal connection line through which signals flow in a ladder-like structure is called a rung, which includes multiple instructions.

![](../_assets/ladder-sample2.png)


A robot teaching project can include one or multiple ladder diagrams, and each diagram may consist of tens to hundreds of rungs.
When the programmable logic controller (PLC) is switched to RUN mode, LD will be executed repeatedly. The time taken to complete one cycle is called scan time and usually ranges from a few milliseconds to several tens of milliseconds.


<br>

An instruction consists of a mnemonic, which is the name of the instruction, and an operand, which is the argument to be transferred to the instruction.

  For example, the ADD (+) instruction in the figure below is configured as follows.

![](../_assets/ladder-add.png)

* Mnemonic: ADD
* Operand1: MW5
* Operand2: DOW2
* Operand3: MW6

<br>

Instructions of an embedded PLC can be classified into multiple instruction groups, as described below. As every instruction will be explained in Section 4, the instructions in this section will be explained as examples for understanding the concept of ladder logic.

---

<br>

## Contact instruction

Classified as a contact instruction, eXamine If Closed (XIC) is a simple instruction with only one operand. This instruction will be indicated on the rung with an operand marked on the -| |- symbol.

![](../_assets/ladder-xic.png)

A contact is a switch determining whether to transfer the signal (1) applied to the left along the rung to the right. If the relay DO3’s value is 0 (inactive), the contact will be open, keeping the signal from being transferred. If the DO3’s value is 1 (active), the contact will be closed, allowing the signal to be transferred.

![](../_assets/ladder-contact.png)

<br>

When several XIC contacts are connected in series or parallel in the form of a branch, logical operational expressions such as AND, OR, and NOT can be created.
(![](../_assets/ladder-not.png) shows an Inverting (INV) instruction that is designed to transfer the opposite value of the logical value on the left to the right and has no operand.)

```
X1 AND (X2 OR (NOT X3))
```

![](../_assets/ladder-and-or-not.png)

<br>


## Output-coil instruction

OuTput Energize (OTE) is classified as an output coil instruction. It is always placed at the rightmost end of the rung and indicated by the -( )- symbol. This instruction allows the value transferred from the left to be outputted to the operand relay.

If the result of the logical operation expression described above is outputted to the Y8 relay, it will be in the form shown below.

```
Y8 = X1 AND (X2 OR (NOT X3))
```

![](../_assets/ladder-ote.png)


<br>

## Function instruction

When the left side becomes active, a specific operation for the given operand will be executed. For example, in the diagram below, when DO3 becomes active, the arithmetic operation ADD (+) of adding the values of MW5 and DOW2 relays and then substituting the thus acquired sum into the MW6 relay will be executed.

```
IF DO3:
   MW6 = MW5 + DOW2
```

![](../_assets/ladder-add2.png)

The compare instruction also transfers the operation result to the right side. For example, in the diagram below, if DO6 becomes active and MW8 exceeds 120, Y20 will be activated.

```
Y20 = DO6 AND (MW8 > 120)
```


![](../_assets/ladder-grt.png)
