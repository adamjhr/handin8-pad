# Handin 8

## Exercise 9.1

(i)

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

## Exercise 9.2

### i

Commands Typed In Console:
```
csc /o StringConcatSpeed.cs
StringConcatSpeed
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