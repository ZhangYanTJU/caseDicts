# caseDicts

OpenFOAM 会自动从某些文件夹中搜索 functionObjects，这些文件夹列在[这里](https://github.com/OpenFOAM/OpenFOAM-dev/blob/master/src/OpenFOAM/db/dictionary/functionEntries/includeFuncEntry/includeFuncEntry.H)。
```
cd ~/.OpenFOAM
git clone git@github.com:ZhangYanTJU/caseDicts.git
```

## 运行时 processing

controlDict 中：

```
functions
{
    #includeFunc autoReconstructPar
    #includeFunc writeCloudOldStyle
}
```

## autoReconstructPar (代码由 Shijie Xu 编写)
OpenFOAM 版本较低时，无法使用 collated fileHandler。
使用此工具可以有效缓解文件数巨量的问题.
正如其名，它会在计算过程中，自动 reconstructPar，然后删掉对应的 decomposed 数据。
此工具只能在 solver 运行时搭配使用。

## [conditionalAverage](https://github.com/ZmengXu/conditionalAverage)
```
postProcess -fields '(Z varZ)' -func conditionalAverage
```

## [writeCloudOldStyle](https://github.com/blueCFD/lagrangianExtraFunctionObjects)
```
sprayFoam -postProcess -func writeCloudOldStyle
find -name positions | while read line; do mv $line $line.coord; mv $line.orig $line; done
find -name positions | while read line; do sed -i -e 's=^\(.*object.*\)positions.orig;=\1positions;=' $line; done
```
如果需要续算，我们要把 positions 改成新格式：
```
find -name positions | while read line; do mv $line $line.orig; mv $line.coord $line; done
```