# POI_geo_analysis
基于POI的地理空间分析

## 研究方法来源：《基于大数据的城市研究与规划方法创新》
尝试复刻情绪值空间分布比较

## 技术步骤
- **数据收集**：评论数量爬取（包括评分、评分细则（如口味、服务等）、评论数（全量、好中差评），评论标签，不含评论内容）。
  
    - 爬虫尝试记录：
      1. **使用selenium**：解决直接用requests无法展开ajax内容的问题
      
      2. **通过配置option抹除chrome webdriver活动特点**：针对 _window.navigator.webdriver == True_
          ```
          option.add_argument("--disable-blink-features")
          option.add_argument("--disable-blink-features=AutomationControlled")
          ```
          爬了快500个以后失败了，用正常浏览器打开网页的反馈是User_Agent啥的，大概是IP被封了，本来打算尝试一下IP池，但是大概隔了10小时又可以上dp了就没在意。
          不过一天之后，在webdriver里即使手动滑块也会被判定“请求异常”，猜测是webdriver的某些特征又被抓取到了，于是尝试第三种方法。
        
      3. **通过mitmdump“中间人”软件监控流量**：针对yoda---.js对webdriver特征的识别，即把js中对webdriver特征串的检测内容替换为其它内容，逃过监测
          (参考了两位大神的博客：https://www.cnblogs.com/lingcai/p/10616311.html, https://blog.csdn.net/u010451638/article/details/109850249)

          (mitmproxy安装参考了：https://blog.csdn.net/qq_37437983/article/details/104319879)

          把以上代码放在.py里，在所在路径运行mitmdump -s flow_editter.py 就可以开始快乐代理啦！

          （留坑）
          
          -- mitmdump原理学习：
          
          -- 爬虫代码：



- 数据处理：核密度？
- 数据分析：相关性分析/聚集度分析/...
- 数据可视化：Python/Echatrs

## 研究目的
借助已有数据+锻炼爬虫能力，进一步熟悉空间分析方法，尝试独立课题探索。
