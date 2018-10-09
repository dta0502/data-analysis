# pyecharts pip安装后出现“No module named 'jupyter echarts pypkg'”错误

## 问题说明
在最开始`import pyecharts`时就报出了
`ModuleNotFoundError: No module named 'jupyter echarts pypkg'`这个错误，其中`jupyter echarts pypkg`库包含包含所有图表组件。

后面使用pyecharts保存得到的`html`文件是空白的。

## 解决方法
先卸载
```bash
pip uninstall jupyter-echarts-pypkg
```
再安装。
```bash
pip install jupyter-echarts-pypkg
```
问题解决！