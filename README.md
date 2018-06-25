# goose --- JAVA版的通用网页正文内容采集器
## 介绍
  本项目是 http://cdmd.cnki.com.cn/Article/CDMD-10614-1016062696.htm  *毛凯 2015年硕士研究生论文* 对应的源代码。
  系统采用的是较流行的 maven 管理依赖， B/S 架构模式。
  该项目主要实现了通用的网页正文内容提取， 只需在系统页面中输入需要提取页面的URL地址，即可得到该网页正文内容，正确率高！<br/>
  此项目主要是借鉴了 python 版本的goose 的原理，通过JAVA技术进行了实现。
  运行方法，将war文件放置到web容器（tomcat的webapps）中，即可运行！
  
## 改进

   有待进一步的改进和完善地方,主要包括以下几个方面: <br />
	1、对于非新闻类的或者正文不集中的HTML页面，本文并不能有效的查找出唯一的最优子树。<br />
		往往只能判断其中某一部分的内容。下一步工作中，可以重点针对页面正文不集中的HTML页面进行算法逻辑的改进。 <br />
	2、本文对正文信息节点的算法主要是利用分词技术对节点中的文本信息分词，然后取出其中的停止词进行分析。<br />
		本系统比较依赖于分词技术的准确性和停止词的一致性。比如下面这段话“梁振英遭到泛民主派和亲北京阵营议员质问”。根据分词技术得到的中词汇如下：<br />
          `梁振英/遭到/泛民主派/和亲/北京/阵营/议员/质问/`
	在停止词表查询得知，这段话中仅有一个词[遭到]属于停止词。且恰巧小于本系统设置的停止词数量阈值`{2}`，那本段话将会看做噪音节点会被本系统过滤掉。 <br/>
	究其原因，其实在于切词系统错误的将[和][亲北京阵营]切成了[和亲][北京][阵营]。当然这并非切词系统的BUG。 <br/>
	因为目前的自然语言处理NLP对这种具有二义性的语义还没有达到人工智能的高度。<br/>
	3、本系统的降噪模块主要是基于社区对海量HTML分析总结出来的非正文节点表，并根据该节点表进行匹配删除。随着大量的新页面的增加，该表也需要同步维护更新。<br/>
	由于上述的问题，后续可以进一步考虑对本系统进行优化。优化主要有两个方向：<br/>
	- 增加信息节点判断的标准来防止正确的文本信息节点被系统过滤掉。
	- 找出更优秀的算法来对系统的降噪处理流程进行补充。
  
  
  
  
  
  
  
	