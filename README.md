# caseDicts

OpenFOAM 会自动从某些文件夹中搜索 functionObjects，这些文件夹列在[这里](https://github.com/OpenFOAM/OpenFOAM-dev/blob/master/src/OpenFOAM/db/dictionary/functionEntries/includeFuncEntry/includeFuncEntry.H)。
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
