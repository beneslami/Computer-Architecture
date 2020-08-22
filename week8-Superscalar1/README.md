Types of Data Hazards

1. Read-After-Write (RAW)

```
r3 <- r1 op r2
r5 <- r3 op r4
```

2. Write-After-Read (WAR)

```
r3 <- r1 op r2
r1 <- r4 op r5
```

3. Write-After-Write (WAW)

```
r3 <- r1 op r2
r3 <- r6 op r7
```

### Superscalar Processor

Superscalar processors enable CPI <1 (IPC > 1) by executing multiple instructions in parallel.

||t1|t2|t3|t4|t5|t6|t7|
|---|---|---|---|---|---|---|---|
|OpA|F  |D  |A0 |A1 |w  |
|OpB|F  |D  |B0 |B1 |w  |
|OpC|   |F  |D  |A0 |A1 |W  |
|OpD|   |F  |D  |B0 |B1 |W  |
|OpE|   |   |F  |D  |A0 |A1 |w  |
|OpF|   |   |F  |D  |B0 |B1 |w  |

Dual Issue Data Hazards:

* No Bypassing:
||t0|t1|t2|t3|t4|t5|t6|t7|t8|
|---|---|---|---|---|---|---|---|---|---|
|ADDIU R1, R1, 1|F|D|A0|A1|W|
|ADDIU R3, R4, 1|F|D|B0|B1|W|
|ADDIU **R5**, R6, 1| |F|D|A0|A1|W|
|ADDIU R7, **R5**, 1| |F|D|D|D|D|A0|A1|W

* Full Bypassing:
||t0|t1|t2|t3|t4|t5|t6|t7|t8|
|---|---|---|---|---|---|---|---|---|---|
|ADDIU R1, R1, 1|F|D|A0|A1|W|
|ADDIU R3, R4, 1|F|D|B0|B1|W|
|ADDIU **R5**, R6, 1| |F|D|A0|A1|W|
|ADDIU R7, **R5**, 1| |F|D|D|A0|A1|W
