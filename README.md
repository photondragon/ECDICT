# ECDICT

Free English to Chinese Dictionary Database.

## 简介

多年前制作的一份英文->中文字典的双解词典数据库，根据各类考试大纲和语料库词频收录 20万条各类单词的英文和中文释义，并按照各类考试大纲和词频进行标注。

## 选词

很多网上词典（如 X明英汉词典，X道词典）号称收词量大（40万），但是很多是些专业名词，光医学名词和化学名词就接近20万，这些平时用的并不多，而平时用的很多的，比如对比中考高考到 GRE的一万五千核心词汇，居然能缺少至少两千词汇，对比英国国家语料库（BNC）的词频数据，前十万高频词汇缺少一万二多，同时对比美国当代语料库前六万高频词汇，任然缺少一万多。

包括不限于国内某些出门的词典，很多号称收词量多，但是他们把词给收偏了，所以我们需要更科学的根据各类考试大纲和语料库进行选词：

避免搞什么大而全的 40万词条，OALD和朗文等也才17万左右的收词量，不要那几十万乱七八糟的来自医学化学电力机械化工等专业的词条，保持20万左右的收词量足够。从最初的中高考各类考试大纲开始，到各种语料库和词频库，选择真正重要的20万词，选词工作参考如下资料：

| 语料库 | 解释 |
|--------|------|
| 考试大纲 | 中考大纲，高考大纲，四六级大纲，托福雅思GRE大纲，等，必须覆盖到位 |
| BNC 词频数据 | 英国国家语料库（British National Corpus）是目前世界上最具代表性的当代英语语料库之一。该语料库书面语与口语并重，其光盘版词次超过一亿，其中书面语语料库9千余万词，口语语料库1千余万词。 |
| Oxford 3K | 《牛津3000词》是“由语言专家和经验丰富的教师根据词频和词意覆盖范围精心挑选的3000词，由于他们的重要性和有用性，被认为是应该最先学习的 |
| 华尔街日报语库 | 根据近20年华尔街日报语库整理而成的杂志类词频顺序表进行选词 |
| 柯林斯星级 | 柯林斯从语料库中将单词在日常生活中的使用频率统计出来，按照频率的高低将单词分级，五星的就是日常生活中最常用的，依次类推。|
| 美国当代语料库 | 前面的 BNC语料库主要收录了近几百年的英文单词，而当代语料库主要收录近20年的电影电视，报刊，谈话记录，文献，小说 等 |
| Urban Dictionary | 俚语俗语等词汇 |



## 双解释义

当然要双解，诸如 WordNet，wiktionary.org 等提供了大量开放的释义资料。同时针对各类考试大纲词汇，网上有不少带释义的单词表供人下载，这些数据有的有错误，有的格式不统一，有的缺音标，有的缺英文释义，有的却中文释义，质量层次补齐，需要书写必要的代码来一次次整理统计，纠正和补全。

索性类似 WordNet 之类的开放语料库提供了针对 Python 的自然语言处理工具包，可以 pip下载下来，直接分析词汇和定义，还有词形变化，反义词近义词等。

释义参考了大量资料，包括不限于：

| 名称 | 解释 |
|------|------|
| 考试大纲 | 网上各种带释义的考试大纲词表（非纸质出版书籍）|
| WordNet | 普林斯顿自然语言处理资料库和工具包 |
| Wiktionary | 多种语言的释义维基百科资料，由各国用户贡献的各类词条 |
| Wikepedia | 维基百科收录了大量词条解释 |
| CEDIT | 中文到英文的开放词典数据库，根据中文到英文的释义，反解出英文到中文的释义 |
| TheFreeDictionary.com | 多语言开放词典 |
| Google | Google Cloud Translation | 
| foldoc.org | Free Online Dictionary Of Computing |
| linguee.com | 数亿词条解释 |
| Babylon | 各类词条数据来源聚合 |
| Urban Dictionary | 俚语俗语释义 |

大量资料需要整合编辑校对，幸好有各种自然语言处理的开发包，可以用来做这件事情，制定评分标准，一个词语多个出处，选择最恰但准确的，核心词汇进行人工校对，部分不全的词条使用英翻中来解决。

## 单词标注

给数据库中每个单词标注：是否是各类考试大纲词汇？以及他们在 BNC和其他语料库里的词频顺序。

## 数据格式

采用 CSV文件存储所有词条数据，用 UTF-8进行编码，用 Excel的话，别直接打开，否则编码是错的。在 Excel里选择数据，来自文本，然后设定逗号分割，UTF-8编码即可。

| 字段 | 解释 |
|------|------|
| word | 单词名称 |
| phonetic | 音标，以英语英标为主，好听嘛 |
| definition | 单词释义（英文） |
| translation | 单词释义（中文）|
| pos | 词语位置，（待添加）|
| collins | 柯林斯星级 |
| oxford | 是否是牛津三千核心词汇 | 
| tag | 字符串标签：zk/中考，gk/高考，cet4/四级 等等标签，空格分割 |
| bnc | 英国国家语料库词频顺序 |
| frq | 当代语料库词频顺序 |
| tense | 时态（ed, ing等）待添加 |
| plural | 复数形式 |
| detail | json 扩展信息 |
| audio | 读音音频 url （待添加）|
| audio_uk | 英语发音 |
| audio_us | 美语发音 |

提供一段 Python 程序来读取这些数据，可以用它转换到 SQLite 和 MySQL 的数据库里，方便你用更高级的方法筛选查询。词条数据大小写不敏感，不论从查询还是排序，还是编程接口。

## 编程接口

代码 stardict.py 用于操作该数据（兼容 Python 2/3），同时实现三个类：

| 类名 | 说明 |
|------|------|
| DictCsv | 用于读写 ecdict.csv 数据格式文件 |
| StarDict | 用来读写 SQLite 词典数据文件，数据字段和上面相同，接口也和 CSV版本相同 |
| DictMySQL | MySQL版本的数据文件读写，同样字段和接口和上面两者相同 |

以上三个类都统一提供如下接口：

| 接口 | 说明 |
|------|------|
| query | 查询单词，可以查整数id（CSV里id为行号，其他两者是自增量）或单词字符串，返回Python字典 | 
| match | 单词匹配，匹配最相似的前 N个单词 |
| query_batch | 批量查询 |
| count | 返回数据库词条总数 |
| register | 注册新单词 |
| update | 更新单词数据，除了 id, word两个字段外其他都可以更新 |
| remove | 删除单词 |
| commit | 提交更改 |


## 参考资料


