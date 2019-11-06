## JavaScript历史
它最初由Netscape的Brendan Eich设计。JavaScript是甲骨文公司的注册商标。Ecma国际以JavaScript为基础制定了ECMAScript标准。JavaScript也可以用于其他场合，如服务器端编程。完整的JavaScript实现包含三个部分：ECMAScript，文档对象模型，浏览器对象模型。
Netscape在最初将其脚本语言命名为LiveScript，后来Netscape在与Sun合作之后将其改名为JavaScript。JavaScript最初受Java启发而开始设计的，目的之一就是“看上去像Java”，因此语法上有类似之处，一些名称和命名规范也借自Java。但JavaScript的主要设计原则源自Self和Scheme。JavaScript与Java名称上的近似，是当时Netscape为了营销考虑与Sun微系统达成协议的结果。为了取得技术优势，微软推出了JScript来迎战JavaScript的脚本语言。为了互用性，Ecma国际（前身为欧洲计算机制造商协会）创建了ECMA-262标准（ECMAScript）。两者都属于ECMAScript的实现。尽管JavaScript作为给非程序人员的脚本语言，而非作为给程序人员的脚本语言来推广和宣传，但是JavaScript具有非常丰富的特性。
发展初期，JavaScript的标准并未确定，同期有Netscape的JavaScript，微软的JScript和CEnvi的ScriptEase三足鼎立。1997年，在ECMA（欧洲计算机制造商协会）的协调下，由Netscape、Sun、微软、Borland组成的工作组确定统一标准：ECMA-262

**以上这些是百度百科百度出来的JavaScript的历史**

### 然后再来说说他的创始人
布兰登·艾奇（Brendan Eich，1961年～），JavaScript的发明人，目前（2005年至2014年）在Mozilla公司担任首席技术长（Chief Technology Officer）。出任Mozilla的CEO十天就被迫辞职
**他就是这样的一个人**
### 主题来了
今天看到一则评论是这样写的：
----------------------
写前端的直接承认就行了，JavaScript 这门语言被 Brendan Eich 搞的就是屎！一！样！的！设！计！

Wiki 上原文：

JavaScript was originally developed in 10 days in May 1995 by Brendan Eich, while he was working for Netscape Communications Corporation. Indeed, while competing with Microsoft for user adoption of Web technologies and platforms, Netscape considered their client-server offering a distributed OS with a portable version of Sun Microsystems's Java providing an environment in which applets could be run.[citation needed] Because Java was a competitor of C++ and aimed at professional programmers, Netscape also wanted a lightweight interpreted language that would complement Java by appealing to nonprofessional programmers, like Microsoft's Visual Basic (see JavaScript and Java).[10]
大意就是 JavaScript 根本就是 Bredan Eich 这一个实习生在短时间内赶工出来的一个目标轻量级的解释形语言。

Bredan Eich 本来是个写 Lisp 的，压根就没搞过 OOP，但是当时网景想借 Java 的“东风”，结果他“苦熬”十天憋出来这么个玩意儿。你能在 JavaScript 里看到很多 Lisp 的影子，感觉它好像是个函数式的。函数式里函数是第一等公民（即所谓的 First-Class Function），函数可以被当作参数传递给另一个函数，这里就涉及到作用域的问题。可是又特么有个不伦不类的 prototype 和 this，又有点儿像 OOP。call 和 apply 就是这种情况下的产物，又像函数式又像 OOP。
呵呵好几个踩我的，都是前端没跑了。

我自己也写前端，写这么多年了谁骂 JS 我给谁点赞。

JS 是屎、可不代表用屎写不出来牛哔的作品来。这都拎不清的我劝你趁早转行。

估计水平不咋地的人看到自己唯一会的一门语言被骂，只会急得跳脚，暗搓搓地点个踩心里再喷两句，也不想想自己写的代码是不是屎上加屎。

--------------------
**首先看到这个我不禁一抖，JavaScript真的是这样吗？**
于是我查查了资料，资料上是这么说的：
网景急于解决浏览器与用户交互这个问题。当时解决这个问题有两个办法，一个是采用现有的语言，比如Perl、Python、Tcl、Scheme等等，允许它们直接嵌入网页。另一个是发明一种全新的语言。
这两个选择各有利弊。第一个选择，有利于充分利用现有代码和程序员资源，推广起来比较容易;第二个选择，有利于开发出完全适用的语言，实现起来比较容易。到底采用哪一个选择，网景公司内部争执不下，管理层一时难以下定决心。
就在这时发生了一件大事，1995年Sun公司将Oak语言改名为Java，正式向市场推出。Sun公司大肆宣传，许诺这种语言可以"一次编写，到处运行"(Write Once, Run Anywhere)，它看上去很可能成为未来的主宰。网景公司动了心，决定与Sun公司结成联盟。它不仅允许Java程序以applet(小程序)的形式，直接在浏览器中运行;甚至还考虑直接将Java作为脚本语言嵌入网页，只是因为这样会使HTML网页过于复杂，后来才不得不放弃。
总之，当时的形势就是，网景公司的整个管理层，都是Java语言的信徒，Sun公司完全介入网页脚本语言的
决策。 因此，Javascript后来就是网景和Sun两家公司一起携手推向市场的，这种语言被命名为"Java+script"并不是偶然的。此时，34岁的系统程序员Brendan Eich登场了。1995年4月，网景公司录用了他。
Brendan Eich的主要方向和兴趣是函数式编程，网景公司招聘他的目的，是研究将Scheme语言作为网页脚本语言的可能性。Brendan Eich本人也是这样想的，以为进入新公司后，会主要与Scheme语言打交道
仅仅一个月之后，1995年5月，网景公司做出决策，未来的网页脚本语言必须"看上去与Java足够相似"，但是比Java简单，使得非专业的 网页作者也能很快上手。 这个决策实际上将Perl、Python、Tcl、Scheme等非面向对象编程的语言都排除在外了。
Brendan Eich被指定为这种"简化版Java语言"的设计师。
**重点内容**
但是，他对Java一点兴趣也没有。为了应付公司安排的任务，他只用10天时间就把Javascript设计出来了。
由于设计时间太短，语言的一些细节考虑得不够严谨，导致后来很长一段时间，Javascript写出来的程序混乱不堪。如果Brendan Eich预见到，未来这种语言会成为互联网第一大语言，全世界有几百万学习者，他会不会多花一点时间呢?
总的来说，他的设计思路是这样的：
(1)借鉴C语言的基本语法;
(2)借鉴Java语言的数据类型和内存管理;
(3)借鉴Scheme语言，将函数提升到"第一等公民"(first class)的地位;
(4)借鉴Self语言，使用基于原型(prototype)的继承机制。
所以，Javascript语言实际上是两种语言风格的混合产物----(简化的)函数式编程+(简化的)面向对象编程。 这是由Brendan Eich(函数式编程)与网景公司(面向对象编程)共同决定的。
如果不是公司的决策，Brendan Eich绝不可能把Java作为Javascript设计的原型。作为设计者，他一点也不喜欢自己的这个作品：
"与其说我爱Javascript，不如说我恨它。它是C语言和Self语言一夜情的产物。十八世纪英国文学家约翰逊博士说得好：'它的优秀之 处并非原创，它的原创之处并不优秀。' (the part that is good is not original, and the part that is original is not good.)"

差不多以上就是JavaScript这门语言比较完整的介绍了，我觉得那个评论者的一句话很对：JS 是屎、可不代表用屎写不出来牛哔的作品来。这都拎不清的我劝你趁早转行
## 最后
反正我是挺喜欢JavaScript这门语言的，但我还是感觉他还是有一点难，可能是因为我学的知识还不够多吧
JavaScript借鉴了那马多的语言的特性，我觉得已经很不错，就这一点，我就觉得它是一门值得去学的语言，更何况经过
 多年的发展，JavaScript从ES到ES再到ES，还有现如今流行的typescript，我总是相信JavaScript的道路会越走越好，就像那句话说的那样：以后能用JavaScript实现的。都将会用JavaScript来实现，还有一点是，现在前端语言除了JavaScript来写脚本，还能用其他什么语言吗？这个问题在JavaScript发明之初就面对过，正因为没有更好的，所以，网景公司才会开发一门新的语言，来写前端脚本，在随着现如今的JavaScript在不断地发展着，相比JavaScript刚问世被骂，被排挤，被浏览器禁用，好的太多太多了，我也相信JavaScript会一直是最优秀的前端脚本语言，最近正在读JavaScript的那本犀牛书，就是JavaScript权威指南，我觉得挺有意思，也正是因为这个，我才慢慢喜欢上了JavaScript，祝JavaScript越来越好，我耶会对JavaScript继续进行学习，JavaScript现如今可是非常获得一门一门语言呢，正如所说的那样：发明者要是知道，JavaScript现在回这吗流行，他应会谨慎考虑而不会用十天时间来完成对他的创作吧，毕竟JavaScript现在可是可以写出十分厉害的东西呢。
哈哈哈，JavaScript，不管别人怎吗骂你，你作为我进入计算机领域的第一门语言（除了HTML，css），我一定不会讨厌你的，现在大二，我估计我大学剩下的两年还是会跟你好好相处的，OK，书写完毕，洗澡去！