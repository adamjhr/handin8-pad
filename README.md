# Handin 8

## Exercise 9.1

### i

Commands typed into console:
```
> csc /o Selsort.cs
> ildasm /text Selsort.exe > Selsort.il
```

The body of Selsort:
```il
 .method public hidebysig static void  SelectionSort(int32[] arr) cil managed
  {
    // Code size       57 (0x39)
    .maxstack  4
    .locals init (int32 V_0,
             int32 V_1,
             int32 V_2,
             int32 V_3)
    IL_0000:  ldc.i4.0              // Push 0 onto stack
    IL_0001:  stloc.0               // i = 0
    IL_0002:  br.s       IL_0032    // Go into for loop
    // The for-loop body begins here
    IL_0004:  ldloc.0               // i on stack
    IL_0005:  stloc.1               // least = i
    IL_0006:  ldloc.0               // i on stack
    IL_0007:  ldc.i4.1              // 1
    IL_0008:  add                   // calculate i + 1
    IL_0009:  stloc.2               // j = i + 1
    IL_000a:  br.s       IL_001a    // Jump into second for loop
    // Second for loop body
    IL_000c:  ldarg.0               // Load arr
    IL_000d:  ldloc.2               // Load j
    IL_000e:  ldelem.i4             // arr[j]
    IL_000f:  ldarg.0               // Load arr
    IL_0010:  ldloc.1               // Load least
    IL_0011:  ldelem.i4             // arr[least]
    IL_0012:  bge.s      IL_0016    // arr[j] < arr[least]
    // Conditional statement is true (next 2 lines)
    IL_0014:  ldloc.2               // Load j
    IL_0015:  stloc.1               // least = j
    IL_0016:  ldloc.2               // Load j
    IL_0017:  ldc.i4.1              // 1
    IL_0018:  add                   // j+1
    IL_0019:  stloc.2               // j = j + 1 (j++)
    IL_001a:  ldloc.2               // Load j
    IL_001b:  ldarg.0               // Load arr
    IL_001c:  ldlen                 // arr.Length
    IL_001d:  conv.i4               // convert to 32 bit
    IL_001e:  blt.s      IL_000c    // j < arr.Length, jump if inner loop is to continue

    IL_0020:  ldarg.0               // Load arr
    IL_0021:  ldloc.0               // Load i
    IL_0022:  ldelem.i4             // arr[i]
    IL_0023:  stloc.3               // tmp = arr[i]
    IL_0024:  ldarg.0               // Load arr
    IL_0025:  ldloc.0               // Load i
    IL_0026:  ldarg.0               // Load arr
    IL_0027:  ldloc.1               // Load least
    IL_0028:  ldelem.i4             // arr[least]
    IL_0029:  stelem.i4             // arr[i] = arr[least]
    IL_002a:  ldarg.0               // Load arr
    IL_002b:  ldloc.1               // Load least
    IL_002c:  ldloc.3               // Load tmp
    IL_002d:  stelem.i4             // arr[least] = tmp
    IL_002e:  ldloc.0               // Load i
    IL_002f:  ldc.i4.1              // 1
    IL_0030:  add                   // i + 1
    IL_0031:  stloc.0               // i = i+1 (i++)
    IL_0032:  ldloc.0               // Load i
    IL_0033:  ldarg.0               // Load arr
    IL_0034:  ldlen                 // arr.Length
    IL_0035:  conv.i4               // Convert the length to 32bit
    IL_0036:  blt.s      IL_0004    // i < arr.Length

    IL_0038:  ret
  } // end of method Selsort::SelectionSort
```

### ii

Commands typed into console:
```
>javac .\Selsort.java
>javap -verbose -c Selsort.class > Selsort.jvmbytecode
```

Body of Selsort.jvmbytecode
```
stack=4, locals=4, args_size=1
//First for header
         0: iconst_0            //push const 0 onto stack
         1: istore_1            //stores the const 0 as var i
         2: iload_1             //loads var i on top of the stack
         3: aload_0             //loads var arr (which was the arg) on top of the stack
         4: arraylength         //pops arr of stack and pushes arr.length on top of the stack
         5: if_icmpge     57    //for comparison, if i >= arr.length, return, else continue in loop

//First for body
         8: iload_1             //loads var i
         9: istore_2            //stores the value of var i as var least

//Second for header
        10: iload_1             //loads var i
        11: iconst_1            //pushes const 1 to stack
        12: iadd                //adds i and 1, aka the value of j, and pushes it to the stack
        13: istore_3            //stores the value of j, as var j
        14: iload_3             //loads var j on top of the stack
        15: aload_0             //loads var arr
        16: arraylength         //pops, value of arr, pushes arr.length
        17: if_icmpge     37    //if j >= arr.length, jump to end of nested for, else continue in nested loop

//Second for body
//if(arr[j] < arr[least])
        20: aload_0             //loads var arr
        21: iload_3             //loads var j
        22: iaload              //loads the value of arr[j]
        23: aload_0             //loads var arr
        24: iload_2             //loads var least
        25: iaload              //loads the value of arr[least]
        26: if_icmpge     31    //if arr[j] >= arr[least], jump past the if body, else continue through the if

//If body
        29: iload_3             //loads var j
        30: istore_2            //store the value of j in least, aka: least = j

//end of if body
        31: iinc          3, 1  //increment var j
        34: goto          14    //check second for header again

//end of second for body
//int tmp = arr[i]; arr[i] = arr[least]; arr[least] = tmp;
        37: aload_0             //load var arr
        38: iload_1             //load var i
        39: iaload              //find arr[i]
        40: istore_3            //store as var tmp (var j is now out of scope, so 3 is free again)
        41: aload_0             //load var arr
        42: iload_1             //load var i
        43: aload_0             //load var arr
        44: iload_2             //load var least
        45: iaload              //find arr[least]
        46: iastore             //store arr[least] as arr[i] (arr[i] = arr[least]) -> iastore arr, i, arr[least]
        47: aload_0             //load arr
        48: iload_2             //load least
        49: iload_3             //load tmp
        50: iastore             //store tmp as arr[least] (arr[least] = tmp)-> iastore arr, least, tmp
        51: iinc          1, 1  //increment var i
        54: goto          2     //Check first for loop header again
        57: return              //returns the SelectionSort function call, to return address saved in stackframe
```

## Exercise 9.2

### i

Commands Typed In Console:
```
>csc /o StringConcatSpeed.cs
>StringConcatSpeed
```

Result:
```
Initialization: Building array of small strings

Concatenate using StringBuilder:
Result length: 168894;    time:   0.000 sec


Press return to continue...


Concatenate using repeated string concatenation:
Result length: 168894;    time:   0.839 sec
```

### ii

Following the given instruction shows that the naive StringConcatSpeed peaked at ~60% of time in GC. This was measured on .NET 7.0

### iii

In order to test this, I checked the % time in GC of and Instance called DSAService, which was running in the background, which Peaked at ~0.1% of time in GC