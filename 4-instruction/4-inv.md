# 4.4 INV (Inverting): Inverting


### Description
Inverts (active <-> inactive) the previous result of the rung.

<br>

### Example of use

According to DeMorgand's law, processing an invert will make /(AxB) equal to /A+/B or /(A+B) equal to /Ax/B, allowing a simple configuration that uses the AND logic that has no branches instead of a configuration that uses the OR logic, which has multiple branches.
As such, the logic of the two rungs below will have the same result because (X1+X2+X3) equals to /(/X1x/X2x/X3).

![](../_assets/inv.png)
