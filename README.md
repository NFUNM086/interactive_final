# 促进或是抑制：探究我国地区互联网发达程度与居民幸福感的关系

#### Pythonanywhere入口

### 研究背景

[“2019中国最具幸福感城市”](https://baike.baidu.com/item/%E4%B8%AD%E5%9B%BD%E6%9C%80%E5%85%B7%E5%B9%B8%E7%A6%8F%E6%84%9F%E5%9F%8E%E5%B8%82/23186310?qq-pf-to=pcqq.temporaryc2c)（由新华社瞭望东方周刊、瞭望智库共同主办）调查推选结果于不久前的11月25日在广州发布。众所周知，“幸福感”对于城市来说十分重要。它意味着居民对所在城市的认同感、归属感、安定感、满足感，以及外界人群的向往度、赞誉度。
而随着互联网的诞生、科技的发展，网络普及程度/电商发展/地区生产总值（GDP）等指标是否影响着当地居民的幸福感，换句话来说，这几种因素的增值是否能提升当地居民情感上的积极影响、提高他们对所在城市的认同度，即对居民幸福感是促进还是抑制，正是我想探究的选题。

### 数据来源

- **国家统计局：**
1. [2010-2016年分省互联网普及率](http://data.stats.gov.cn/easyquery.htm?cn=E0103)
2. [2000-2018年分省电商销售额](http://data.stats.gov.cn/easyquery.htm?cn=E0103)
3. [2000-2018年分省GDP](http://data.stats.gov.cn/easyquery.htm?cn=E0103)

- **百度百科：**
1. [中国最具幸福感城市2007-2019年排行榜（新华社瞭望东方周刊、瞭望智库共同主办）](https://baike.baidu.com/item/%E4%B8%AD%E5%9B%BD%E6%9C%80%E5%85%B7%E5%B9%B8%E7%A6%8F%E6%84%9F%E5%9F%8E%E5%B8%82/23186310?fr=aladdin)

### 数据清理

1. [2010-2016年分省互联网普及率（%）表格](https://github.com/NFUNM086/interactive_final/blob/master/internet.csv)
2. [2013-2018年分省电商销售额（亿元）表格](https://github.com/NFUNM086/interactive_final/blob/master/E_sales.csv)
3. [2014-2018年分省GDP（亿元）表格](https://github.com/NFUNM086/interactive_final/blob/master/GDP.csv)
4. [2012-2019年中国最具幸福感城市前十排行榜](https://github.com/NFUNM086/interactive_final/blob/master/happiness_times_draft.csv)
5. [2012-2019中国最具幸福感城市入榜（前五）次数](https://github.com/NFUNM086/interactive_final/blob/master/happiness_times.csv)

### 可视化过程

```python
***数据清洗***
互联网普及率2016 = list(zip(list(dfi.province),list(dfi.year_2016)))  # 转换为列表
# print (互联网普及率2016)
电商销售额2018 = list(zip(list(dfs.province),list(dfs.year_2018)))  
# print (电商销售额2018)
GDP2018 = list(zip(list(dfg.province),list(dfg.year_2018)))
# print(GDP2018)
happiness = list(zip(list(dfh.province),list(dfh.times)))
# print(happiness)

from pyecharts import options as opts
from pyecharts.charts import Scatter


# 2012-2019中国最具幸福感城市推选评比入榜（前五）次数散点图
def scatter_base() -> Scatter:
    c = (
        Scatter(init_opts=opts.InitOpts(width="2500px", height="800px"))
        .add_xaxis(list(dfh.province))
        .add_yaxis("次数", list(dfh.times))
        .set_global_opts(title_opts=opts.TitleOpts(title="2012-2019最具幸福感城市推选评比上榜（前五）次数"))
    )
    return c
scatter_base().render_notebook()


# 2016中国分省互联网普及率热力图
from pyecharts import options as opts
from pyecharts.charts import Geo
from pyecharts.globals import ChartType, SymbolType

def geo_heatmap() -> Geo:
    c = (
        Geo()
        .add_schema(maptype="china")
        .add(
            "互联网普及率",
            互联网普及率2016,
            type_=ChartType.HEATMAP,
        )
        .set_series_opts(label_opts=opts.LabelOpts(is_show=False))
        .set_global_opts(
            visualmap_opts=opts.VisualMapOpts(),
            title_opts=opts.TitleOpts(title="2016中国分省互联网普及率热力图"),
        )
    )
    return c
分省互联网普及率热力图 = geo_heatmap()
分省互联网普及率热力图.render_notebook()
```


### 故事阐述和概括

通过分省互联网普及率、电商销售额、GDP这三种维度的数据与“最具幸福感城市”上榜次数进行比较，结果发现这三者和城市的“幸福感”并无直接关系，也就是说，**一个城市的经济发展水平越高、网络科技越发达，不代表当地居民的幸福感越强烈。**

在分析过程中，发现近十年来浙江省的宁波和杭州这两所城市一直榜上有名，并且近几年有逐步上升的趋势，而天津市虽在2012-2014年连续上榜，却从2015年开始便没有再出现在榜内。于是我把浙江省和天津市拎出进行具体的对比，发现**一个地区的电商发展情况与该城市的幸福感有一定的相关关系。**

### 思考和总结

在这个信息科技大爆炸的年代，电商平台随网络发展而顺应崛起，可以说“网购”方便了很多人的生活，节约了不少工厂的资源成本，也通过网络连结到很多底层人民的生活。在一个电商发达的城市里，人民的生活更加便利、物质和精神需求更能得到满足。同时，电商行业的振兴也带来了很多前所未有的机会——网购、网络营销，再者，跟电商相关的领域和行业也将会迎来新的机遇，如直播带货、摄像器材等等。**综上所述，电商的发展给当地居民带来情感上或多或少的积极影响。**

### 故事洞见

快乐是人类生活与经济发展的终极目标，是衡量经济发展成功的最高指标。同样，幸福感对于城市来说也十分重要。通过以上数据清理分析和可视化呈现，不难发现**居民所在城市幸福感与GDP、互联网普及率、电商销售额并无直接的正相关关系。但城市的电商发展一定程度上影响着该地居民的幸福感。**

科学发展观下的社会发展不再仅仅是关注经济的增长，也不是以现代化为终极目标，而是切实回归以人为本的层面，关注民生问题，关注人民的感受。**通过此次的数据交互可视化，我发现居民的幸福感和GDP、互联网普及率无正相关关系，即当地生产总值、互联网发达程度不能作为衡量当地居民幸福感的标准。若该市政府想要提升居民幸福感，不仅要关注经济建设，还需需提高文化建设、社会保障、精神需求、竞争压力等社会问题。**


### 参考文献
1. [关于城市居民幸福感的调查报告](https://wenku.baidu.com/view/5244144d6aec0975f46527d3240c844769eaa08e.html)

2. [要GDP，更要幸福感](https://www.ixueshu.com/document/15c1dea339bdbfb1318947a18e7f9386.html)

3. [如何看待越来越发达的互联网反而让大众感到生活焦虑？_问答_极智能](https://www.ziiai.com/question/42)

4. [智能科技越发达越先进，为什么我们的幸福感却越低？！_凤凰科技](http://tech.ifeng.com/a/20171021/44724563_0.shtml)



