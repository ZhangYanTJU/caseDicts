# caseDicts

```
cd ~/.OpenFOAM
git clone git@github.com:ZhangYanTJU/caseDicts.git
```

## 使用-运行时

controlDict 中：

```
functions
{
    #includeFunc autoReconstructPar
    #includeFunc spanwiseAverageForMixtureFraction
}
```

## 使用-运行后

```
postProcess -latestTime -func sampleLineForMixtureFraction -field Z
postProcess -latestTime -func sampledCuttingPlane

```
