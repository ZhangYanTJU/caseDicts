# caseDicts

User defined configuration files of functionObjects, you can put this directory [here](https://github.com/OpenFOAM/OpenFOAM-dev/blob/master/src/OpenFOAM/db/dictionary/functionEntries/includeFuncEntry/includeFuncEntry.H).
One example is `~/.OpenFOAM/caseDicts/postProcessing`.

```
cd ~/.OpenFOAM
git clone git@github.com:ZhangYanTJU/caseDicts.git
```

You can use these configuration files directly once you put then on the [specified place]((https://github.com/OpenFOAM/OpenFOAM-dev/blob/master/src/OpenFOAM/db/dictionary/functionEntries/includeFuncEntry/includeFuncEntry.H)).
Or you can just copy them into your `$FOAM_CASE/system`.


## [autoReconstructPar, from ZmengXu](https://github.com/ZmengXu/autoReconstructPar)

If you cannot use `collated fileHandler`, you may generate huge amount of files.
This code will save you from this.
It will auto `reconstructPar `on the fly, and delete the corresponding decomposed data.
**And it must be used on the fly.**

In your controlDict:
```
functions
{
    #includeFunc autoReconstructPar
}
```


## [conditionalAverage, from ZmengXu](https://github.com/ZmengXu/conditionalAverage)

```
postProcess -fields '(Z varZ)' -func conditionalAverage
```

## [writeCloudOldStyle, from blueCFD](https://github.com/blueCFD/lagrangianExtraFunctionObjects)

Another contribution from [ZmengXu](https://github.com/ZmengXu/lagrangianExtraFunctionObjects/tree/OF5x), enables the code to write both ascii and binary format, which has not been merged yet.

### For the finished case:
```
sprayFoam -postProcess -func writeCloudOldStyle
find -name positions | while read line; do mv $line $line.coord; mv $line.orig $line; done
find -name positions | while read line; do sed -i -e 's=^\(.*object.*\)positions.orig;=\1positions;=' $line; done
```

### On the fly:

In your controlDict:
```
functions
{
    #includeFunc writeCloudOldStyle
}
```

### continue your simulation
If you want to continue your case, you should change the `positions` to the new format:
```
find -name positions | while read line; do mv $line $line.orig; mv $line.coord $line; done
```

## histogram

```
postProcess -func histogram
```
