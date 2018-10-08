# pyecharts地理坐标系 出现显示不全或只显示南海诸岛问题

```python
from pyecharts import Geo, Map
 
province_distribution = {'河南': 45, '北京': 97, '河北': 21, '辽宁': 12, '江西': 6, '上海': 20, '安徽': 10, '江苏': 16, '湖南': 9, '浙江': 13, '海南': 2, '广东': 22, '湖北': 8, '黑龙江': 11, '澳门': 1, '陕西': 11, '四川': 7, '内蒙古': 3, '重庆': 3, '云南': 6, '贵州': 2, '吉林': 3, '山西': 12, '山东': 11, '福建': 4, '青海': 1, '舵主科技，质量保证': 1, '天津': 1, '其他': 1}
 
province_keys=province_distribution.keys()
province_values=province_distribution.values()
 
map = Map("我的微信好友分布", "@SilenceYaung",width=1200, height=600)
map.add("", province_keys, province_values, maptype='china', is_visualmap=True,
visual_text_color='#000')
map.render()

```

一切准备就绪，然后执行代码，出现了显示不全或只显示南海诸岛问题。

官网给的解释如下：自从 0.3.2 开始，为了缩减项目本身的体积以及维持 `pyecharts`项目的轻量化运行，`pyecharts`将不再自带地图 js 文件。如用户需要用到地图图表，可自行安装对应的地图文件包。

下面介绍如何安装：
- 全球国家地图: [echarts-countries-pypkg (1.9MB)](https://github.com/pyecharts/echarts-countries-pypkg):世界地图和 213 个国家，包括中国地图。
- 中国省级地图: [echarts-china-provinces-pypkg (730KB)](https://github.com/pyecharts/echarts-china-provinces-pypkg)：23 个省，5 个自治区。
- 中国市级地图: [echarts-china-cities-pypkg (3.8MB)](https://github.com/pyecharts/echarts-china-cities-pypkg)：370 个中国城市。

需要这些地图的朋友，可以装 pip 命令行:
```bash
pip install echarts-countries-pypkg
pip install echarts-china-provinces-pypkg
pip install echarts-china-cities-pypkg
```
特别注明，中国地图在 `echarts-countries-pypkg `里。
