#### 以下部分由贺君完成：

# 3 
## *存在链接错误时的捕获-再捕获方法*
Loredana Di Consiglio
Istat，国家统计局，罗马，意大利

Tiziana Tuoto
Istat，国家统计局，罗马，意大利

张丽春
南安普敦大学，挪威统计局，奥斯陆大学



目 录

3.1 简介 ............................................................................................40  
3.2 捕获-再捕获模型：简短的形式化记号 .................................................................40  
3.3 联动模型和联动误差 ...............................................................................42    
    3.3.1 Fellegi和Sunter的联系模式 ..................................................................42  
    3.3.2 链接误差的定义和估计 ........................................................................44  
    3.3.3 记录联系的贝叶斯方法 ........................................................................45  
3.4 存在链接错误时的DSE ...............................................................................47    
    3.4.1 Ding和Fienberg的估计器 .....................................................................47  
    3.4.2 修改后的Ding和Fienberg估计器 ...............................................................48  
    3.4.3 一些评论 ...................................................................................49  
    3.4.4 例子 .......................................................................................52  
3.5 在多个列表的情况下进行链接错误调整 .................................................................57  
    3.5.1 基于对数线性模型的估计器 ....................................................................57  
    3.5.2 一种替代性的建模方法 ........................................................................60  
    3.5.3 一个贝叶斯的建议 ............................................................................61  
    3.5.4 例子 .......................................................................................62  
3.6 结语 .............................................................................................65  
参考文献 .............................................................................................66



## 3.1 简介
种群规模估计的标准方法是由[45]和[37]提出的捕获-再捕获法，并在[14]、[43]、[46]和[52]、[53]中进行了回顾。对人类种群事件的应用可以追溯到1949年[54]。该方法被应用于人类人口的评估，例如，人口普查中少计的规模（见[63]，[64]，[24]，[27]，[30]），受特定疾病或使用非法药物影响的人数[4]，内战中的受害者人数[3]。参见[7]关于社会和医学科学中最近收集的捕获-再捕获法。一个传统的研究重点是假设重新捕获的同质性或独立性。对异质性或名单依赖性的考虑，可以在例如[40]、[6]、[10]、[67]中找到。参见，例如，[20]中的贝叶斯方法。

$\quad\quad$ 最近，在基于多个行政登记册而不是传统的人口普查的基础上产生类似人口普查的统计数据方面，捕捉-捕获方法的使用受到越来越多的关注。这突出了另外两个方法上的挑战。首先，行政登记册除了少计外，还可能包含大量错误的统计（范围外的个人）；例如，见第8章和第9章。其次，在许多应用中，并不存在一个可以用来连接所有行政登记册的唯一标识符，在这种情况下，链接年龄误差是不可避免的，而通常提出的完美匹配的假设被违反了。在本章中，我们将集中讨论这个问题，并研究不同的建议，这些建议通过隐含地考虑到链接误差来调整捕获-捕获估计。

$\quad\quad$ 本章的组织结构如下：第2节简要叙述了捕获-再捕获模型及其假设，并介绍了本章其余部分使用的符号。第3节回顾了一些常见的频繁主义和贝叶斯记录联系方法和联系误差的相关估计。第4节和第5节介绍了对两个或更多名单的捕获-俘获估计的修正方法。其中包括一些例子，以说明链接误差对种群估计偏差的影响，并展示所建议的调整方法的收益。最后，第6节提供了一些结论性意见和未来工作的方向。

## 3.2 捕获-再捕获模型：简短的形式化和符号化
捕获-再捕获法估计人口的未知规模（N），需要比较两个（或更多）目标人口单位的查点清单，以计算每个清单中 "捕获 "的单位数量，以及在任何清单组合中 "重新捕获 "的单位数量。

表3.1
两份名单中的计数的列联表
<table>
	<tr>
	    <th colspan="2">  </th>
	    <td colspan="2">名单2</th> 
	</tr >
	<tr >
	    <td colspan="2" >  </td>
	    <td>目前</td>
	    <td>缺失</td>
	</tr>
    <tr >
	    <td rowspan="2">名单1</td>
	    <td>目前</td>
	    <td>n11</td>
        <td>n10</td>
	</tr>
    <tr >
	    <td>缺失</td>
	    <td>n01</td>
        <td>n00</td>
	</tr>
</table>


表3.2
基于三份名单的计数的列联表
<table>
	<tr>
	    <th >  </th>
	    <td colspan="4">名单1</th> 
	</tr >
	<tr >
	    <td  >  </td>
	    <td colspan="2">目前</td>
	    <td colspan="2">缺失</td>
	</tr>
    <tr >
	    <td  >  </td>
	    <td colspan="2">名单3</td>
	    <td colspan="2">名单3</td>
	</tr>
    <tr >
	    <td >名单2</td>
	    <td>目前</td>
	    <td>缺失</td>
        <td>目前</td>
	    <td>缺失</td>
	</tr>
    <tr >
	    <td>目前</td>
	    <td>n111</td>
	    <td>n110</td>
        <td>n011</td>
        <td>n010</td>
	</tr>
    <tr >
	    <td>缺失</td>
	    <td>n101</td>
	    <td>n100</td>
        <td>n001</td>
        <td>n000</td>
	</tr>
</table>

以两个列表为例。 $n_{1+}$ 和 $n_{+1}$ 分别为第一和第二份名单中的人口单位数。 $n_{11}$ 是两份名单中的单位，因此 $n_{10}$ = $n_{1+}$ - $n_{11}$ 是只在名单1中的单位数， $n_{01}$ = $n_{+1}$ - $n_{11}$ 是只在名单2中的单位数。这些计数可以组织在一个2x2的列联表3.1中，其中 $n_{00}$ 是两份名单中遗漏的（不可观察的）单位数。

$\quad\quad$ 所谓的人口规模N的双系统估计器（DSE）由以下公式给出：

$$
\begin{array}{c} 
\widetilde{N}_p=n_ {1+} \times n_ {+1}/n_ {11}
\end{array}
$$<p align="right">(3.1)</p>

DSE可以用各种方式来激励。例如，见[63]对相关假设的讨论。与我们后面的讨论特别相关的是，如果被列在名单1中的概率对所有人口单位都是恒定的，那么这个同质（即恒定）的捕获概率的估计值由以下公式给出：

$$
\begin{array}{c} 
\widetilde{{\pi}}_{1,p}=n_ {11} / n_ {+1}
\end{array}
$$<p align="right">(3.2)</p>

同样地，只要名单2中的捕获量是同质的，我们有：

$$
\begin{array}{c} 
\widetilde{{\pi}}_{2,p}=n_ {11} / n_ {1+}
\end{array}
$$<p align="right">(3.3)</p>

$\quad\quad$ 作为特例的DSE，可以基于K-列表捕获-再捕获数据的对数线性模型[22]得出一个更普遍的方法。特别是，由于结构上的零元素数，即所有列表中缺失的单位，我们必须将涉及所有K因子的交互项设为零。Fienberg[22]表明，未观察到的元素的最大似然估计（MLE）可以用一个简单的通用表达式给出。
对于表2的情况，这变成了：

$$
\begin{array}{c} 
\widetilde{{n}}_{00}=n_ {10} \times n_{01}/ n_ {11}
\end{array}
$$<p align="right">(3.4)</p>

$\quad\quad$ 由此可见，N的MLE由 $\widetilde{N}_ {ML} = n + \widetilde{n}_ {00} = \widetilde{N}_ p$ 给出，其中 n = $n_{11}$ + $n_{10}$ + $n_{01}$ 。因此，让列表3的捕获-再捕获计数按表3.2的方式排列，用 $n_{ijk}$ 表示，i, j, k = 0, 1。 然后，MLE由 $\widetilde{N}_ {ML} = n+\widetilde{n}_ {000}$ ，其中

$$
\begin{array}{c} 
\widetilde{{n}}_ {000}={n_ {111} n_ {001} n_ {100} n_ {010} \over n_{101}n_{011}n_{101}}
\end{array}
$$<p align="right">(3.5)</p>

## 3.3 联动模型和联动误差
$\quad\quad$ 因此，捕获-再捕获法的一个关键步骤是确定两个（或多个）名单中的共同单位，这被称为记录联系。在这一节中，我们描述了概率记录联系的框架，主要是为了正式确定联系误差的定义和估计。

### 3.3.1 Flellegi和Sunter联动模型
$\quad\quad$ Fellegi和Sunter[21]的开创性论文中给出了记录联系的频繁主义理论。我们参考Herzog等人[29]的全面阐述。给定两个列表，例如 $L_1$ 和 $L_2$ ，大小为 $N_1$ 和 $N_2$ ，让 $\Omega$ ={(a,b), a $\in$ $L_1$ 且 b $\in$ $L_2$ }是所有可能配对的完整集合，大小 | $\Omega$ | = $N1 \times N2$ 。 $L_1$ 和 $L_2$ 之间的记录联系被视为一个分类问题，通过这个问题， $\Omega$ 中的配对被分配到两个子集，M和U，独立且互斥，这样：
M是链接集（a=b）。
U是非链接集（a $\neq$ b）。

$\quad\quad$ 选择共同的标识符（链接变量），对于每一对，应用一个比较函数，以获得相应的比较向量，用 $\gamma$ 表示。让r成为 $\gamma$ 属于M集合时的条件概率与 $\gamma$ 属于U集合时的条件概率之间的比率，它是 $H_0$ : (a, b) $\in$ M 与 $H_1$ : (a, b) $\in$ U的似然统计，即:

$$
\begin{array}{c} 
\ r={P(\gamma|(a,b)\in M) \over P(\gamma|(a,b)\in U)}={m(\gamma) \over u(\gamma)}
\end{array}
$$<p align="right">(3.6)</p>

因此，那些r大于上限阈值 $T_m$ 被分配到链接配对集的配对， $M^∗$ ；r小于下限阈值 $T_u$ 被分配到非链接配对集的配对， $U^∗$ ；如果r在范围内（ $T_u$  ,  $T_m$ ），则不会自动做出决定，配对将通过审查进行分类。

$\quad\quad$ 阈值的选择是为了最小化虚假链接概率（用 $\beta$ 表示）和虚假非链接概率（用1- $\alpha$ 表示），其定义如下：

$$
\begin{array}{c} 
\ \beta=\sum\limits_{\gamma \in \Gamma}u(\gamma)P(M^* | \gamma)=\sum\limits_{\gamma \in \Gamma_{M^* }} u(\gamma)  \quad\quad 当\Gamma_{M^*}=\lbrace\gamma:T_m\leq m(\gamma)/u(\gamma) \rbrace
\end{array}
$$<p align="right">(3.7)</p>

$$
\begin{array}{c} 
\ 1-\alpha=\sum\limits_{\gamma \in \Gamma}m(\gamma)P(U^* |\gamma)=\sum\limits_{\gamma \in \Gamma_{U^* }}u(\gamma)\quad\quad 当\Gamma_{U^* }=\lbrace\gamma:T_u\geq m(\gamma)/u(\gamma) \rbrace
\end{array}
$$<p align="right">(3.8)</p>

$\quad\quad$ 在应用中，概率m和u可以通过将真实的链接状态视为潜在变量并使用EM算法来估计。将真正的链接状态作为一个潜在的变量，并使用EM算法[33]。改变了原有的做法后，[34]应用贝叶斯潜质类和贝叶斯对数线性模型来拟合混合模型[36]。

$\quad\quad$ 对于有两个以上文件的情况，存在一些同步记录链接可以实现；见[50], [49], [55], [62] , [25]。然而，使这些方法可以扩展到人口数据集的 "工业强度"应用，目前仍然是一个开放的问题。一个合理的方法是对所涉及的列表进行配对链接。然而，一个关键的困难是，单独的列表成对链接并不能保证链接决策的可传递性。例如，假设在3个列表问题中，列表1中的记录a与列表2中的b基于上述的方法被链接，而b与3个列表中的记录c基于单独的2个列表链接被链接，但a和c没有基于单独的2个列表链接被链接。这种情况可能发生，因为每两个列表的链接错误都有自己的接受阈值。现在有5种可能的 "决定"：a、b和c指的是同一个；a和b指的是同一个但c指的是另一个；a和c指的是同一个但b指的是另一个；b和c指的是同一个但a指的是另一个；所有a、b和c指的是不同的人。然而，没有任何逻辑方法可以将这5类的分类还原为三个两类的分类，以一种转义的方式。

$\quad\quad$ 因此，对于多个文件的记录链接，一个普遍的做法是首先创建一个主框架。然后将其余的每一个列表逐一单独链接到主框架上。例如，我们可以从链接列表1和列表2开始，然后将得到的框架与列表3链接。这种程序的优点是只需要两个链接操作，不需要解决差异问题，而成对的方法需要三个链接操作，需要解决差异问题，如上所述。根据所描述的两步过程，让1 - $\alpha_1$ 为第一次操作中遗漏链接的概率，1 - $\alpha_2$ 为第二次操作的概率；此外，让 $\beta_1$ 为第一次操作中出现错误链接的概率， $\beta_2$ 为第二次操作的概率。我们在第5节中假设了这种方法。


### 3.3.2 链接误差的定义和估计
两种类型的链接错误，即虚假的联系和遗漏的匹配，在调整基于联系数据的统计分析中起着核心作用，包括捕获-再捕获估计器。然而，在实践中众所周知，尽管Fellegi和Sunter[21]的决策规则方法对链接识别非常有效，但公式（3.7）和（3.8）对误差 $\beta$ 和1- $\alpha$ 的评估通常不太可靠。注意，在概念上，通过（3.7）和（3.8），参数 $\beta$ 和1- $\alpha$ 是为交叉产品比较的每个元素定义的 $\Omega$ = $L_1$ $\times$ $L_2$ ，显然，这个定义没有考虑到任何链接程序所固有的相互依赖性，（对于这里处理的一般情况） $L_1$ 中的一条记录可能与 $L_2$ 中的一条以上的记录相联系，反之亦然。因此，对于联系数据的统计分析，应该避免使用 $\beta$ 和1- $\alpha$ 的估计值，这些估计值是为了方便决策规则而产生的，而应该进行联系后的评估，以适应实际联系的相互依赖性。Tuoto[61]提出了一种监督学习方法来预测这两种类型的链接错误，而不像[5]那样依赖于强分布假设。另一种方法[11]将两种类型的链接错误，即虚假的联系和遗漏的匹配，在调整基于联系数据的统计分析中起着核心作用，包括捕获-再捕获估计器。然而，在实践中众所周知，尽管Fellegi和Sunter[21]的决策规则方法对链接识别非常有效，但公式（3.7）和（3.8）对误差 $\beta$ 和1- $\alpha$ 的评估通常不太可靠。注意，在概念上，通过（3.7）和（3.8），参数 $\beta$ 和1- $\alpha$ 是为交叉产品比较的每个元素定义的 $\Omega$ = $L_1$ $\times$ $L_2$ ，显然，这个定义没有考虑到任何链接程序所固有的相互依赖性，（对于这里处理的一般情况） $L_1$ 中的一条记录可能与 $L_2$ 中的一条以上的记录相联系，反之亦然。因此，对于联系数据的统计分析，应该避免使用 $\beta$ 和1- $\alpha$ 的估计值，这些估计值是为了方便决策规则而产生的，而应该进行联系后的评估，以适应实际联系的相互依赖性。Tuoto[61]提出了一种监督学习方法来预测这两种类型的链接错误，而不像[5]那样依赖于强分布假设。另一种方法[11]将自举法应用于实际链接程序，以评估错配概率，其中链接的相互依赖性的影响被复制到自助法的链接结果中。

$\quad\quad$ 接下来，撇开估计问题不谈，采用比那些适用的链接误差更方便或必要的定义。在（3.7）和（3.8）中。例如，考虑（3.1）中的DSE， $n^∗_{11}$ 算是列表1和列表2之间的链接记录的数量，这与真实记录的数量有关。匹配 $n_{11}$ 的两个数字： $n_{11}$ 真正匹配中错过的匹配数。，以及 $n^∗_11$ 实际链接中的虚假链接的数量。

$\quad\quad$ 在实践中，错过匹配的概率可以用以下方法定义：分母( $N_1$ - $n^{* }_ {11}$)+( $N_2$ - $n^{∗}_ {11}$ )，这是列表1或2中未链接的记录的数量而不是 $U^{* }$ 的大小，也就是说，所有链接中没有实现。请注意， $U^{* }$ 是一个比( $N_1$ - $n^∗_{11}$ )+( $N_2$ - $n^∗_{11}$ )大得多的集合。此外，值得注意的是，人们可以预期虚假链接的数量包括要比未链接的记录之间的错误链接的数量低得多的实际链接的记录的数量，因为前者意味着同时存在两个链接错误，即错过真正的匹配和错误地将匹配记录链接到不同的记录。

$\quad\quad$ 应该指出的是，以这种方式定义的虚假链接率是一个与用于调整回归分析的虚假匹配率不同的数量（例如，在[8]中），后者是与实际链接的数量 $n^∗ _ {11}$ 有关的。虽然两者的目标是在所做的链接中找到相同数量的虚假链接，这两个比率是不一样的，因为它们的分母不同。

$\quad\quad$ 最后，值得注意的是，这两类的相关性也不同，可能有误差。以DSE（3.1）为例，很明显，  $n^{∗ }_ {11}$ 在实际链接中应调整由于缺失的匹配而向上，但由于虚假链接而向下。对种群规模的估计，决定这两个错误之间的平衡是 $n^{∗ }_ {11}$ 而不是 $n_{11}$ ，其中DSE可能是过度或不足的。请注意，在实践中，往往更容易减少错误链接率，例如，通过使用更严格的接受标准。然而，这将不可避免地增加缺失匹配的数量。在许多对动物种群的研究中，基于从自然标记（如自然标签、照片、DNA指纹）中识别单个动物，由于链接程序的谨慎，虚假链接的概率通常可以忽略不计。

### 3.3.3 记录的贝叶斯方法链接
[26]、[35]和[36]考虑了记录链接的贝叶斯方法。具体来说，在[26]和[39]的方法中，感兴趣的数量是一个矩阵值的参数C，它代表两个列表之间的真实匹配模式。然后，C的元素之和是对两个列表之间真实匹配数量的估计，前提是对
C的参数空间的限制，以避免多重匹配：

$$
\begin{array}{c} 
\ C_{ij}\in\lbrace0,1 \rbrace\quad\quad \sum\limits_{L_1}C_{ij}\leq1\quad\quad\sum\limits_{L_2}C_{ij}\leq1 
\end{array}
$$<p align="right">(3.9)</p>

$\quad\quad$ 对于分层贝叶斯设置，顶层可以是比较向量 $\gamma$ ，如[26]，其中 $\gamma$ 被假定为具有多叉分布，参数为 $m$ 或 $u$ ，取决于 $C_{ij}$ 为1或0。随机向量 $m$ 或 $u$ 被假定为相互独立,且独立于C，并且由于计算原因，遵循Dirichlet分布。另外，[39]和[59]直接提出了联系变量的模型，而不是比较向量。命中-失误模型的一个变形（见[13]）被用来模拟可能的失真过程，随后是均匀的随机重化，即联系变量的观察值给定其真实值。

$\quad\quad$ 在中间层次上，假设在两个列表的捕获-再捕获情况下，真实匹配的数量 $n_{11}$ 遵循超几何分布（[59]），给定目标人群规模N和两个列表的规模。矩阵C
的分布在其可能的结果空间上是均匀的，给定 $n_{11}$ 。同时，真实链接变量的向量遵循一个合适的Urn分布，给定 $n_{11}$ ，由目标种群的随机抽样产生。

$\quad\quad$ 最后，在底层，真实联系变量向量的种群分布可以通过考虑目标种群作为无限超级种群的随机样本，以及相关参数及其先验分布来建模。为了完成的规范性，我们需要一个N的先验分布。Liseo和Tancredi[39]把p(N) $\propto$ 1/ $N^2$ 截断在{1,   $N^{* }$ }上，其中 $N^{* }$ 是一个合理的极大值。Tancredi和Liseo[59]使用 $p_g(N)$ $\propto$ $\Gamma$ (N-g+1)/N！对于g $\geq$ 0，其中较大的g将较低的先验权重放在右尾。


#### 以下部分由周沐阳完成：

$\quad\quad$ 与Fellegi和Sunter [21]的方法不同，贝叶斯方法并不将不同记录对的匹配视为彼此不相关的，这是合乎逻辑的。在实践中，需要在初始链接步骤（[33]）之后施加一个线性约束，以避免在Fellegi和Sunter [21]的决策规则方法下可能存在的多个链接。贝叶斯公式更自然地考虑了通过矩阵C的约束。最后，根据贝叶斯的观点进行推理，该方法允许人们将链接过程的不确定性传播到后续的链接数据分析中，这将在第3.4节中所示。

$\quad\quad$贝叶斯方法的一个实际困难是缺乏对大型数据集的可扩展性，就像在类似人口普查的人口规模估计的情况下一样。从理论上讲，目标参数N的先验分布的选择似乎有些随意。在[59]的激励2列表例子中，我们有$\left(n_{1+}, n_{+1}\right)=(34,45)$，其中$n_11^* = 25&对有完全匹配的链接变量。na ̈ıve DSE是61，这可能是由于缺少匹配而高估的;而45将是N的下界，假设没有错误的枚举。由于没有信息，建议的先验不考虑这种考虑。结果N的后验中位数为55，97.5%分位数为65，后者似乎na ̈ıve DSE相当高。无论如何，尚不清楚结果对先验分布、信息性或非信息性有多敏感。

$\quad\quad$Steorts等人[55]提出了另一种贝叶斯方法，它允许同时链接和删除来自多个列表的记录。这个想法（类似于[44]）是将记录链接看作是一个识别单独文件背后的真正潜在"实体"的过程。因此，每个记录指一个目标人口单位（即潜在实体），由一个整数从1到Nmax表示，称为链接结构，其中Nmax是所有列表的记录总数，所以在极端情况下列表可以没有共同的实体。所有引用同一实体的记录都是"链接的"。假设连杆结构的先验分布是均匀。建模方法在其他方面与上述概述的方法类似。采用混合MCMC算法生成连杆结构的后验分布。引入了最可能最大匹配集的规则，保证了多个列表匹配的传递性。详情请参阅[57]。

$\quad\quad$对于基于捕获-再捕获数据的种群大小估计，[57]的方法原则上允许根据它们的后验分布采样细胞计数，如表3.1和3.2中的样本。例如，附加到一个记录中的潜在实体只在该列表中捕获，附加到两个记录中的潜在实体在这两个列表中捕获，以此类推。如果每个记录都附加到至少一个潜在实体，细胞计数集可以形成捕获-再捕获数据，以拟合对数线性模型，从而得出种群大小估计。

$\quad\quad$[60]在相同的贝叶斯设置中扩展了[57]，通过将种群大小作为模型参数，允许在多列表记录链接和重复数据删除问题中进行种群大小估计。
他们观察到，在统一之前的单位（即独立随机抽样替换人口N），样本标签的分布N诱发分布分区空间（即不同的潜在个体的数量）取决于N，从而估计标签的分区将允许同时产生推理N和估计连锁结构。该模型具有完整的先验性$$P{N}=\frac{1}{Z{g}N^g} \qquad （1<N<+∞)$$
其中Z （g）是黎曼泽塔函数。同样，连锁结构的先验（均匀）分布的选择并不适应捕获-再捕获概率的不同情况。如果能够建立并合并对数线性模型的条件单元概率的信息先验分布，它可能会更有用。
## 3.4存在链接错误时的DSE
### 3.4.1Ding和Fienderg估计器
[32]研究了连锁误差对捕获-再捕获估计的影响。在存在连锁错误的情况下，覆盖率，如（3.2）和（3.3），以及人口规模的估计，如（3.1），可能会有偏差，需要进行调整。在2个列表的情况下，[19]提出了一种修正彼得森估计器的方法。[32]$n=n_11^* + n_10^* + n_01^*$根据表3.1给出，但基于连锁数据，其中$n_{1+}^* = n_{1+}$和$n_{+1}^* = n{+1}$。使用N∗11而不是n11的面值DSE通常是有偏倚的。给定n的（n∗11，n∗10，n∗01）的条件似然为$$L{\pi_11^*，\pi_10^*，\pi_01^*}= \frac{n！}{{n_11^*}！{n_10^*}！{n_01^*}！}\frac{{\pi_11^*}^{n_11^*}{\pi_10^*}^{n_10^*}{\pi_01^*}
{n_01^*}}{{{\pi_11^*}+{\pi_10^*}+{\pi_01^*}}^n}$$ 其中，$\pi_10^* = \pi_1^* - \pi_11^*$和$\pi_01^* = \pi_2^* - \pi_11^* = \pi_2 - \pi_11^*$
为了将这些参数与连锁误差联系起来，Ding和finberg（1994）做出了以下假设：

1.有一个假设的链接方向，其中L1链接到L2，即，对于L1中的每一个记录，如果可能的话，我们可以在L2中找到一个链接，而不是相反;

2.L1和L2之间的真实链接的概率为α;

3.涉及L1中匹配记录的错误链接可以忽略不计，涉及L1中不匹配记录的错误链接发生的概率为β。
 

$\quad\quad$请注意，除了链接相互依赖关系外，真实匹配率与（3.8）相同，但错误链接率与（3.7）不相同。在DSE的这些附加假设下，我们有$\pi_{11}^{*}=\alpha \pi_{1} \pi_{2}+\beta \pi_{1}\left(1-\pi_{2}\right)$其中这两项分别来自n11和n10。最大化关于π1和π2的条件似然（3.10），对于给定的β和α值，第一个列表的估计覆盖范围由$$\hat{\pi}_{1, D F}=\frac{-n_{11}^{*}+\beta\left(n_{11}^{*}+n_{10}^{*}\right)}{(\beta-\alpha)\left(n_{11}^{*}+n_{01}^{*}\right)}=\left(\frac{1}{n_{+1}}\right)\left(\frac{n_{11}^{*}-\beta n_{1+}}{\alpha-\beta}\right)$$
第二个列表是由$$\hat{\pi}_{2, D F}=\frac{-n_{11}^{*}+\beta\left(n_{11}^{*}+n_{10}^{*}\right)}{(\beta-\alpha)\left(n_{11}^{*}+n_{10}^{*}\right)}=\left(\frac{1}{n_{1+}}\right)\left(\frac{n_{11}^{*}-\beta n_{1+}}{\alpha-\beta}\right)$$

$\quad\quad$将（3.11）和（3.12）与（3.2）和（3.3）进行比较，可以确定（3.11）和（3.12）的通用项为真实匹配数的链接误差调整估计。由此
可见，N的条件MLE，也是调整后的彼得森估计量，由$$\tilde{N}_{D F}=(\alpha-\beta) \frac{n_{1+} n_{+1}}{n_{11}^{*}-\beta n_{1+}}=\frac{(\alpha-\beta) n_{11}^{*}}{n_{11}^{*}-\beta n_{1+}} N_{p}^{*}$$
其中，$\hat{N_p^*}$是直接使用n 的面值DSE;参见[19]
### 3.4.2修改后的Ding和Fienberg估计器
Di Consiglio和Tuoto[16]提出了一种推广，放宽了单向链接的限制。管理来源的链接激发了这种需求。请注意，丁和芬伯格。
[19]处理的是传统的人口普查覆盖率不足评估，即人口普查计数和计数后调查之间的联系是在一个方向上工作的。当不是单向链接时，L1和L2中不匹配的记录可能会出现错误链接，因此由于后者，我们使用了一个附加项的$\pi_{11}^{*}=\alpha \pi_{1} \pi_{2}+\beta \pi_{1}\left(1-\pi_{2}\right)+\beta \pi_{2}\left(1-\pi_{1}\right) \\$

$\quad\quad$保留上述关于连锁误差的其他假设，最大化条件似然（3.10），对于给定的β和α值，修正的覆盖率的Ding和feng（MDF）估计分别由，$$\hat{\pi}_{1, M D F}=\frac{2 \beta n_{11}^{*}+\beta x_{10}^{*}+\beta n_{01}^{*}-n_{11}^{*}}{(2 \beta-\alpha)\left(n_{11}^{*}+n_{01}^{*}\right)}=\left(\frac{1}{n_{+1}}\right)\left(\frac{n_{11}^{*}-\beta\left(n_{1+}+n_{+1}\right)}{\alpha-2 \beta}\right)$$ $$\hat{\pi}_{2, M D F}=\frac{2 \beta n_{11}^{*}+\beta n_{10}^{*}+\beta n_{01}^{*}-n_{11}^{*}}{(2 \beta-\alpha)\left(n_{11}^{*}+n_{10}^{*}\right)}=\left(\frac{1}{n_{1+}}\right)\left(\frac{n_{11}^{*}-\beta\left(n_{1+}+n_{+1}\right)}{\alpha-2 \beta}\right)$$同样，（3.14）和（3.15）的共同项是n11的连锁误差调整估计，因此MLE，也是n的调整彼得森估计，由$$\tilde{N}_{M D F}=(\alpha-2 \beta) \frac{n_{1+} n_{+1}}{n_{11}^{*}-\beta\left(n_{1+}+n_{+1}\right)}=\frac{(\alpha-2 \beta) n_{11}^{*}}{n_{11}^{*}-\beta\left(n_{1+}+n_{+1}\right)} \tilde{N}_{p}^{*}$$

$\quad\quad$如上所述，DF和MDF估计器都是基于链接误差总体上是恒定的假设。如果这一假设至少在子群中成立，那么估计量可以应用于连锁误差概率（和捕获概率）比在整个种群中更均匀的地层中。

$\quad\quad$当假定错误率已知时，可以考虑真实值n11，n10，n01是由$n_{11}^*$，$n_{10}^*$，$n_{01}^*$的代数确定地得到的。那么，MDF的方差估计量与标准的DSE方差估计量（见[63]）相同，它是由$$\hat{V}\left(\tilde{N}_{M D F}\right)=N \frac{\left(1-\hat{\pi}_{1}\right)\left(1-\hat{\pi}_{2}\right)}{\hat{\pi}_{1} \hat{\pi}_{2}}$$其中，$\hat{\pi}_{1}=\hat{n}_{11} / n_{+1}$和$\hat{\pi}_{2}=\hat{n}_{11} / n_{1+}$在[58]中也采用了同样的方法来校正捕获-重捕获双样本丰度估计器，以解释识别中的假阴性误差。此外，他们还引入了一种自举方法来估计修正估计量的方差。自助法允许合并连锁错误率的估计不确定性。   
### 3.4.3一些评论
下面我们在存在连锁误差的情况下对DSE进行一些评论，并在没有连锁误差的情况下对其与DSE的偏差和方差进行比较。

$\quad\quad$首先，在DSE估计器的标准动机下，两个列表都被认为是随机的，独立枚举，每个都具有恒定的覆盖率，分别用τ1和τ2表示。我们已经$$\left\{\begin{array}{l}
E\left(n_{1+}\right)=N \tau_{1} \\
E\left(n_{+1}\right)=N \tau_{2} \\
E\left(n_{11}\right)=N \tau_{1} \tau_{2}
\end{array} \quad \Rightarrow \quad \frac{E\left(n_{1+}\right) E\left(n_{+1}\right)}{E\left(n_{11}\right)}=N \Rightarrow \hat{N}=\frac{n_{1+} n_{+1}}{n_{11}}\right.$$ 正如[65]和[66]所示的那样，一个更简单的动机是对待其中一个列表，比如列表1是固定的，它需要更少的假设，更适合来自管理来源的列表。假设随机n+1，与在整个目标种群中的恒定捕获率，我们以n1+为条件，$$\left\{\begin{array}{c}
E\left(n_{1+} \mid n_{1+}\right)=n_{1+} \\
E\left(n_{+1} \mid n_{1+}\right)=E\left(n_{+1}\right)=N \tau \\
E\left(n_{11} \mid n_{1+}\right)=n_{1+} \tau
\end{array} \quad \Rightarrow \quad \frac{n_{1+} E\left(n_{+1}\right)}{E\left(n_{11} \mid n_{1+}\right)}=N \quad \Rightarrow \hat{N}=\frac{n_{1+} n_{+1}}{n_{11}}\right.$$我们将在下文中采用这种简化的条件观点。

$\quad\quad$设α为列表1和列表2之间的匹配包含在链接的关节子集中的概率。设β为列表1或列表2中不匹配的记录包含在链接的关节子集中的概率。我们有$$E\left(n_{11}^{*} \mid n_{1+}\right)=\alpha E\left(n_{11} \mid n_{1+}\right)+\left[n_{1+}-E\left(n_{11} \mid n_{1+}\right)\right] \beta+\left[E\left(n_{+1}\right)-E\left(n_{11} \mid n_{1+}\right)\right] \beta \\
=(\alpha-2 \beta) E\left(n_{11} \mid n_{1+}\right)+\left[n_{1+}+E\left(n_{+1}\right)\right] \beta$$给定（α，β），我们可以得到以下估计量$$\hat{n}_{11}=\hat{n}_{11}(\alpha, \beta)=\frac{n_{11}^{*}-\beta\left(n_{1+}+n_{+1}\right)}{(\alpha-2 \beta)}$$ $$\hat{N}(\alpha, \beta)=\frac{n_{1+} n_{+1}}{\hat{n}_{11}(\alpha, \beta)}$$这与（3.16）中的MDF估计器相同。β= 0的特殊情况是特别有趣的，例如，在动物丰度估计下，我们有$$\hat{N}(\alpha)=\hat{N}(\alpha, 0)=\frac{\alpha n_{1+}{ }_{+1}}{n_{11}^{*}}$$

$\quad\quad$下面我们对$n_{+1}$的调整$\hat{N}$DSE(α)和标准DSE进行了明确的比较。这是应用DSE的通常情况，前提是观察并考虑每个单一源的计数。有和没有连锁误差之间的差异是观察$n_{11}^*$或$n_{11}$之间。对于标准的DSE$\hat{N}$，$$\hat{N}=\frac{n_{1+} n_{+1}}{n_{11}} \approx \frac{n_{1+} n_{+1}}{E\left(n_{11} \mid n_{1+}, n_{+1}\right)}-\frac{n_{1+} n_{+1}}{E\left(n_{11} \mid n_{1+}, n_{+1}\right)^{2}}\left[n_{11}-E\left(n_{11} \mid n_{1+}, n_{+1}\right)\right] \\
+\frac{1}{2} \frac{2 n_{1+} n_{+1}}{E\left(n_{11} \mid n_{1+}, n_{+1}\right)^{3}}\left[n_{11}-E\left(n_{11} \mid n_{1+}, n_{+1}\right)\right]^{2}$$ $$E\left(\hat{N} \mid n_{1+}, n_{+1}\right) \approx \frac{n_{1+} n_{+1}}{E\left(n_{11} \mid n_{1+}, n_{+1}\right)}-\frac{n_{1+} n_{+1}}{E\left(n_{11} \mid n_{1+}, n_{+1}\right)^{3}} V\left(n_{11} \mid n_{1+}, n_{+1}\right)$$ $$V\left(\hat{N} \mid n_{1+,} n_{+1}\right) \approx \frac{\left(n_{1+} n_{+1}\right)^{2}}{E\left(n_{11} \mid n_{1+,} n_{+1}\right)^{4}} V\left(n_{11} \mid n_{1+,} n_{+1}\right)$$

$\quad\quad$我们有n11个∼Bin（$n_{+1}$，$n_{1+}$/N）条件为（$n_{+1}$，$n_{1+}$），因为在列表2中枚举列表1内或列表外的记录的概率是相同的。因此，$E\left(n_{11} \mid n_{1+} n_{+1}\right)=n_{1+} n_{+1} / N$和$V\left(n_{11} \mid n_{1+}, n_{+1}\right)=n_{+1}\left(\frac{n_{1+}}{N}\right)\left(1-\frac{n_{1+}}{N}\right)$，从而$$E\left(\hat{N} \mid n_{1+}, n_{+1}\right) \approx N+\frac{N}{\hat{N}^{2}} n_{+1} \frac{n_{1+}}{N}\left(1-\frac{n_{1+}}{N}\right)=N+O(1)$$ $$V\left(\hat{N} \mid n_{1+}, n_{+1}\right) \approx \frac{N^{2}}{\hat{N}^{2}} n_{+1} \frac{n_{1+}}{N}\left(1-\frac{n_{1+}}{N}\right)$$其中，我们假设$\frac{n_{1+}}{N}=\frac{n_{+1}}{N}=\frac{N}{N}=O(1)$为N→∞。接下来，对于(α)，我们也有$$E\left(\hat{N}(\alpha) \mid n_{1+}, n_{+1}\right) \approx \frac{\alpha n_{1+} n_{+1}}{E\left(n_{11}^{*} \mid n_{1+} n_{+1}\right)}-\frac{\alpha n_{1+} n_{+1}}{E\left(n_{11}^{*} \mid n_{1+}, n_{+1}\right)^{3}} V\left(n_{11}^{*} \mid n_{1+}, n_{+1}\right)$$ $$V\left(\hat{N}(\alpha) \mid n_{1+}, n_{+1}\right) \approx \frac{\left(\alpha n_{1+} n_{+1}\right)^{2}}{E\left(n_{11}^{*} \mid n_{1+}, n_{+1}\right)^{4}} V\left(n_{11}^{*} \mid n_{1+}, n_{+1}\right)$$由于$n_{11}^*$∼Bin（$n_{11}$，α）条件是$n_{11}$和$n_{11}$∼Bin（$n_{+1}$，$n_{1+}$/N）条件（$n_{+1}$，$n_{1+}$），我们有$n_{11}^*$∼Bin（$n_{+1}$，α$n_{1+}$/N）条件（$n_{+1}$，$n_{1+}$）。因此，$E\left(n_{11}^{*} \mid n_{1+}, n_{+1}\right)=\alpha n_{1+} n_{+1} / N$和$V\left(n_{11}^{*} \mid n_{1+}, n_{+1}\right)=n_{+1}\left(\alpha n_{1+} / N\right)\left(1-\alpha n_{1+} / N\right)$，这样$$E\left(\hat{N}(\alpha) \mid n_{1+} n_{+1}\right) \approx N+\frac{N}{\hat{N}(\alpha)^{2}} n_{+1} \frac{\alpha n_{1+}}{N}\left(1-\frac{\alpha n_{1+}}{N}\right)=N+O(1)$$ $$V\left(\hat{N}(\alpha) \mid n_{1+}, n_{+1}\right) \approx \frac{N^{2}}{\hat{N}(\alpha)^{2}} n_{+1} \frac{\alpha n_{1+}}{N}\left(1-\frac{\alpha n_{1+}}{N}\right)$$

$\quad\quad$由此可见，$\hat{N}$(α)的条件偏差和方差，即存在连锁误差的方差，与$\hat{N}$的条件偏差，即没有连锁误差的顺序相同。然而，如果$n_{1+}$/N和α都接近于1，我们就有了$$V\left(n_{11}^{*} \mid n_{1+}, n_{+1}\right)>V\left(n_{11} \mid n_{1+}, n_{+1}\right)$$也就是说，当$\hat{N}$（1−α）$\hat{n}_{11}$=（$n_{1+}$+$n_{+1}$−2$\hat{n}_{11}$）β时，我们有$\hat{n}_{11}=$n_{11}^*$，也就是说，如果两种类型的链接错误发生“相互抵消”。为了衡量$\hat{n}_{11}$的期望和方差，让$$n_{11}^{*}=n_{11}^{*}(1,1)+n_{11}^{*}(0,1)+n_{11}^{*}(1,0)$$依次来自列表1和列表2之间的匹配，列表2中不匹配的记录，以及列表1中列表2中不匹配的记录。有条件的（$n_{+1}$，$n_{1+}$），我们有$$n_{11}^{*}(1,1) \sim \operatorname{Bin}\left(n_{+1}, \alpha n_{1+} / N\right)$$ $$n_{11}^{*}(0,1) \sim \operatorname{Bin}\left(n_{+1}, \beta\left(1-n_{1+} / N\right)\right)$$
同样的$$n_{11}^{*}(1,0) \sim \operatorname{Bin}\left(n_{1+},\left(1-n_{+1} / N\right) \beta\right)$$ 由此得出结论$$E\left(n_{11} \mid n_{1+}, n_{+1}\right)=(\alpha-2 \beta) \frac{n_{1+} n_{+1}}{N}+\left(n_{1+}+n_{+1}\right) \beta$$ $$E\left(\hat{n}_{11} \mid n_{1+}, n_{+1}\right)=\frac{n_{1+} n_{+1}}{N}$$ $$E\left(\hat{N}(\alpha, \beta) \mid n_{1+}, n_{+1}\right)=N+\frac{N}{\hat{N}(\alpha, \beta)^{2}} V\left(\hat{n}_{11} \mid n_{1+}, n_{+1}\right)$$

$\quad\quad$观察$n_{11}^*$（1、1）、$n_{11}^*$（0、1）和$n_{11}^*$（1、0）不相互独立，例如，较小n11偶然使较小$n_{11}^*$（1、1）和较大$n_{11}^*$（0、1）和$n_{11}^*$（1、0）同时更可能。

$\quad\quad$虽然V（$\hat{n}_{11}$|$n_{1+}$，$n_{+1}$）在分析上似乎难以处理，但可以通过蒙特卡罗模拟来计算它。我们推测\mid V\left(\hat{n}_{11}^{1} \mid n_{1+}, n_{+1}\right) / N=O(1)渐近为N→∞，，在这种情况下，$\hat{N}$（α，β）的偏差和方差与标准DSE$\hat{N}$.的偏差和方差的顺序相同。
### 3.4.4例子
下面我们将给出一些存在连锁错误的两个例子。

$\quad\quad$例子1。考虑[23]表3.3和3.4中的数据，有三个来源：1990年美国人口普查，相应的后普查调查（PES），行政清单补充，圣路易斯的PES抽样层（ALS）。表3.3给出了Census-PES捕获-再捕获数据，而匹配误差研究（[42]）的结果见表3.4。  
   表3.3  
1990年美国人口普查，第11层，圣路易斯，美国人口普查<h4></h4>   
<table border="1" width="500px" cellspacing="10">
<tr>
<td colspan="2" align="center"></td>
  <td colspan="2" align="center">人口普查</td>
</tr>
<tr>
  <td></td>
  <td></td>
  <td>目前</td>
  <td>缺失</td>
</tr>
<tr>
  <td> PES</td>
  <td>目前</td>
  <td>487</td>
  <td>129</td>
</tr>
<tr>
  <td></td>
</td>
  <td>缺失</td>
  <td>217</td>
  <td>-</td>
</tr>
</tr>
</table>


#### 以下是由黄钰完成的：

### 3.4.4 例子
下面我们将介绍一些存在链接错误的两列表示例。\
$\quad\quad$ 例一：考虑表 $3.3$ 和 $3.4$ 中来自 $[23]$ 的数据,资料来源: $1990$ 年美国人口普查，相应的普查后枚举 $(PES)$ ，行政清单补充 $(ALS)$ ，用于 $PES$ 抽样在圣路易斯的第 $11$ 层普查，人口普查-$pes$捕获-再捕获数据载于表 $3.3$ ，匹配误差研究 $([42])$ 的结果见表 $3.4$ 。

**表3.3**
人口普查和 $PES$ 样本数据 $11$ 层，圣路易斯， $1990$ 年美国人口普查
<table>
<tr>
  <td colspan="2" align="center"></td>
  <td colspan="2" align="center">人口普查</td>
</tr>
<tr>
  <td colspan="2" align="center"></td>
  <td>目前</td>
  <td>缺失</td>
</tr>
<tr>
  <td>PES</td>
  <td>目前</td>
  <td>487</td>
  <td>129</td>
</tr>
<tr>
 <td></td>
 <td>缺失</td>
  <td>217</td>
  <td>-</td>
</tr>

</table>

**表3.4**
圣路易斯复赛研究
<table>
<tr>
  <td rowspan="2" align="center">原始匹配分类</td>
  <td colspan="3" align="center">复配分类</td>
  <td></td>
</tr>
<tr>
 <td>匹配</td>
  <td>不匹配</td>
  <td>未解决的</td>
  <td>总计</td>
</tr>
<tr>
  <td>匹配</td>
  <td>2667</td>
  <td>7</td>
  <td>8</td>
  <td>2682</td>
</tr>
<tr>
 <td>不匹配</td>
 <td>9</td>
  <td>427</td>
  <td>30</td>
  <td>466</td>
</tr>
<tr>
 <td>未解决的</td>
 <td>0</td>
  <td>7</td>
  <td>20</td>
  <td>27</td>
</tr>
<tr>
 <td>总计</td>
 <td>2676</td>
  <td>441</td>
  <td>58</td>
  <td>3175</td>
</tr>

</table>

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({ tex2jax: {inlineMath: [['$', '$']]}, messageStyle: "none" });
</script>

$\quad\quad$ 将复赛结果视为真实，忽略未解决的情况，如 $[23]$ ，失配率为 $1-\hat{\alpha}=9/(2667+9)=0.3363 \% $ ，假链接率是 $\hat{\beta}=7/(7+427)=1.6129 \% $ 。表 $3.3$ 的标准 $DSE$ 结果为 $890$ ，标准误差 $(SE)$ 为 $10.25$ 。结合连杆误差，我们得到 $ \widetilde {N}_{DF}=891$ (以及 $SE=10.29$ )。由于错误率低，调整很小，并且根据 $SE_s$ ，两个估计值没有显著差异。请注意，由于丢失匹配的比率非常低，原始的 $DSE$ 实际上是向上调整的。\
$\quad\quad$ 将两个错误率直接代入 $(3.16)$ ， $MDF$ 估计值为 $ \widetilde {N}_{MDF}=898$ (以及 $SE=10.64$ )。但是，鉴于表 $3.3$ 实际上是由 $PES$ 与人口普查的单向联系产生的，在这种情况下 $MDF$ 估计数是无效的，就像它提到的 $5.5 \approx(129+217) \times \beta$ 487个实际链接中的虚假链接，而数字为 $2 \approx 129 \times \beta$ 符合单向联动程序。这里只计算$MDF$估计及其$SE$，以说明所涉及的计算。\
$\quad\quad$ 例二： 考虑$[16]$中描述的案例，其中有来自两个道路事故死亡事件登记册的数据。由于它们的尺寸较小，可以通过文书审查对链接结果进行完整的分析。道路意外登记册$(RAR)$记录了道路意外的动态和情况，并与死因登记册 $(RCD)$ 相连。关联过程并不简单:没有通用的个人识别代码，而且由于$RAR$参考单位是道路事故，当涉及多人时，个人识别变量(即姓名、姓氏、年龄)有时会丢失或错误。$RAR$有$4237$条记录，$RCD$有$4642$条记录。用于联系的变量包括道路交通受害者/死者的姓名、姓氏和年龄，以及事故/死亡的日期、月份、直辖市和省份。数据大小不需要缩减程序，所有可能的记录对都被检查。可能链接的整个空间也通过文书审查来探索概率过程所遗漏的链接。链接过程标识$3129$条链接记录。估计$Fellegi-Sunter (FS)$联动错误率为$(3.7)和(3.8)$，由 $ \hat { \beta }=0.00$ 和 $1-\hat{\alpha}=0.15$ 得出。通过联动后对联动状态的文书复核，我们可以评估真实的联动错误率(表$3.5$)，其中真实的 $1−\alpha$ 为 $0.1141$ ， $\beta$ 为 $0.0011$ 。

**表3.5**
真实联动状态与概率联动结果的比较
<table>
<tr>
  <td colspan="2" rowspan="2" align="center"></td>
  <td colspan="2" align="center">真实联动状态</td>
  <td rowspan="2" align="center">总计</td>
</tr>
<tr>
  <td>匹配</td>
  <td>不匹配</td>
</tr>
<tr>
<td rowspan="2" align="center">概率联系</td>
  <td>联系</td>
  <td>3127</td>
  <td>2</td>
  <td>3129</td>
</tr>
<tr>
 <td>不联系</td>
 <td>403</td>
  <td>-</td>
  <td>2621</td>
</tr>
<tr>
  <td colspan="2" align="center">总计</td>
 <td>3530</td>
  <td>1819</td>
  <td></td>
</tr>
</table>

此外，使用经过文员审查的真实链接，道路死亡总人数的死亡影响指数为$5572$，而现有的死亡影响指数为$6286$。\
$\quad\quad$由$MDF$估计器得到的种群规模估计为$5571$使用真实的链接错误率，而使用$FS$估计的错误率为$5330$。正如可以预料的那样，$DF$估计值实际上与$MDF$估计值相同，因为$\beta$几乎为零。然而，$DF$估计器在非零的假链接率下是无效的，因为在这种情况下，链接过程不是单向的。原始的$DSE$是高估的，几乎完全是由于错过匹配，这是偏差的主要来源。\
$\quad\quad$值得注意的是，$\beta$和$1-\alpha$的评价并不是直接的，当真正的联动状态仅为一个训练集所知时的链接，但不是所有可能链接的整个空间。例如，众所周知的$[5]$方法只提供了$\beta$的估计值。$[61]$提出的方法对$\beta$和$1-\alpha$进行了估计，但没有对连杆权值进行强分布假设。\
$\quad\quad$例三： 本例说明了计算野生动物种群的贝叶斯不确定性传播。数据报告在$[38]$中，收集自美国弗吉尼亚州谢南多亚山谷的大理石纹蝾螈研究(详细信息见$[2]$)。在本研究中，捕获是通过背部模式的照片来实现的，并使用计算机辅助模式匹配软件来识别个体并构建捕获-再捕获数据(表$3.6$)。在$9$月初成年蝾螈产卵的池塘迁徙前后进行了两次捕捉。

**表3.6**
在美国弗吉尼亚州谢南多亚山谷重新捕获大理石纹蝾螈
<table>
<tr>
  <td rowspan="2" align="center">第一次捕获</td>
  <td colspan="2" align="center">第二次捕获</td>
  <td rowspan="2" align="center">总计</td>
</tr>
<tr>
  <td>目前</td>
  <td>缺失</td>
</tr>
<tr>

  <td>目前</td>
  <td>174</td>
  <td>22</td>
  <td>196</td>
</tr>
<tr>
 <td>缺失</td>
 <td>383</td>
  <td>-</td>
  <td></td>
</tr>
<tr>
  <td>总计</td>
 <td>537</td>
  <td></td>
  <td></td>
</tr>
</table>

$\quad\quad$如前面所提到的，在像这样的生态学研究中，错误的主要风险是对自然标签的错误识别，即缺失匹配率 $\alpha$，根据链接$[38]$的术语产生“幽灵”记录。这样，确定的匹配值就会过低，而估计的种群大小就会过高。\
$\quad\quad$表$3.6$中的数据有四个未知参数，分别是两种情况下的捕获概率$\pi1$和$\pi2$，总体规模$N$和误识别错误率$\alpha$。该模型已超过参数化。$Link$等人$(2010,p.183)$考虑了几种选择:\
$1.$忽略$\alpha$，应用最原始的$DSE$;\
$2.$在$\pi1$=$\pi2$约束下，拟合$\alpha$模型;\
$3.$对$\alpha$进行贝叶斯分析。

根据表$3.6$中的数据，第二种选择显然是不可防御的。第一种选择实际上是第三种选择的特殊情况，在$\alpha$上有一个点质量更优。$[38]$在咨询了现场专家后，确定了$\pi1$、$\pi2$和N的均匀先验，$\alpha$的$\beta(19,1)$先验分布表明了较高但不完美的识别率。然而，$\alpha$的均匀、$\beta(10,1)$、$\beta(19,1)$先验导致几乎相同的$95\%$可信区间，详情见$[38]$。\
$\quad\quad$表$3.7$提供了结果的摘要。N的后验分布由吉布斯采样器$([38])$得到。给出了$N$后验分布的中位数、第$2.5^{th}$百分位和第97.5百分位$\alpha$的先验。为了进行比较，还计算了$MLE$和相关的置信度，将预期$\alpha$在其先验分布下处理，就好像它是已知的一样。请注意，最后一行中的$MLE$对应于原始的$DSE$，它忽略了识别错误，而调整后的$MLE$不能为第一行中的期望值$\alpha$计算，因为调整后的真匹配数大于第一次捕获的总数。

**表3.7**
$\alpha$备选先验下$N$的估计值
| $\alpha$ 的先验    | $N$ 的后中位数（ $2.5^{th}$ , $97.5th$ 百分位）    | $\alpha$ 期望值    | $MLE$ 和 $0.05 \% $ 置信区间     |
| -------- | -------- | -------- |-------- |
| $\beta(1,1)$ | $569(538,616)$ | $0.50$ |-|
| $\beta(10,1)$ | $573(538,618)$ | $0.91$ | $550(540,560)$ |
| $\beta(19,1)$ | $578(539,620)$ | $0.95$ | $575(557,502)$|
| $\beta(100,1)$ | $595(557,628)$ | $0.99$ | $599(575,623)$|
| $\beta(\infty,1)$ | $606(585,636)$ | $1$ | $605(580,630)$|

$\quad\quad$我们注意到置信区间的长度随着$\alpha$而减小，如果$\alpha$是已知的，这是可以理解的，因为它意味着真实匹配的数量是已知的，并且在两个列表大小固定的情况下不断增加。然而，在这种情况下，将规定的$\alpha$视为已知的显然是误导。贝叶斯后验不确定性随着$\alpha$的先验期望的降低而增加，这是由于先验分布在其中心周围变得不那么集中。对于比$\beta(19,1)$更不确定的先验，结果表明$(i)$后验$95\%$区间相对于先验的选择是稳健的，$(ii)$后验中位数是比后验均值更稳健的点估计选择。\
$\quad\quad$例三： 为了进行比较，在$[16]$中提出了仿真研究不同联动情景下的估计量，突出了标准捕获-再捕获估计的偏差。模拟中使用的虚构数据模拟了覆盖范围不足的寄存器以及链接变量$[41]$中存在的错误。这两份清单分别根据 $\tau_1= 0.930$和 $\tau_2= 0.924$随机生成。这两个列表被连接在一起，假设了三种不同的情况。黄金情景使用具有最高识别能力的链接变量，即姓名、苏尔$(Sur)$名称、完整出生日期。这在错误率方面给出了最好的结果，其中$\alpha=0.939， \beta=0.001$。银色场景代表了最强有力的可识别变量(即姓名和姓氏)不可用的情况，例如，由于隐私保护可能会出现这种情况。链接过程以完整出生日期为基础。这导致了比黄金情景更高的链接错误率，其中 $\alpha=0.851，\beta=0.101$。最后，青铜场景在链接错误方面是最不利的，由于附加的链接变量的错别字和缺失值。所得$\alpha$和$\beta$的平均值分别为$0.833和0.108$。有原始的$DSE$,$DF$和$MDF$估计量彼此比较，其中$DF$和$MDF$估计器是使用每次复制中的$\alpha$和$\beta$的真实值计算的。结果还与不受连锁误差影响的真实$DSE$进行了比较。\
$\quad\quad$在黄金情景中，假链接误差几乎不存在，恰当的估计器减少了原始$DSE$的偏差，正如可以预期的那样，在这种情况下$DF$和$MDF$非常接近。在银色场景中，虚假链接率$\beta$不再可以忽略，$MDF$明显优于形成替代估计器，其中$DF$估计器是不合适的，因为链接不是单向的。$MDF$估计器的改进在具有较高假链接率的青铜场景中更加明显。有关复制设置和结果的详细信息，请参见$[16]$。

**表3.8**
3-list链接单元计数表
<table>
<tr>
  <td></td>
  <td colspan="4" align="center">列表1</td>
</tr>
<tr>
  <td></td>
  <td colspan="2" align="center">目前</td>
  <td colspan="2" align="center">缺失</td>
</tr>
<tr>

  <td></td>
  <td colspan="2" align="center">列表3</td>
  <td colspan="2" align="center">列表3</td>
</tr>
<tr>
 <td>列表2</td>
 <td>目前</td>
  <td>缺失</td>
  <td>目前</td>
  <td>缺失</td>
</tr>
<tr>
  <td>目前</td>
 <td>n*111</td>
  <td>n*110</td>
  <td>n*011</td>
  <td>n*010</td>
</tr>
<tr>
  <td>缺失</td>
 <td>n*101</td>
  <td>n*100</td>
  <td>n*001</td>
  <td>n*000</td>
</tr>
</table>

## 3.5 在多个列表的情况下，链接错误调整
本节研究了连锁误差的影响，并提出了基于第$3.2$节中介绍的多次重捕获和线性模型的群体规模估计量的调整。

### 3.5.1 基于对数线性模型的估计器
我们从表$3.8$中的$3$列表链接数据开始，其中$n^*_{ijk}$是基于链接数据的单元数，$\pi^*_{ijk}$​是对应的单元概率，对于$i,j,k=1,0,$$n^*_{ijk}$​根据定义是不可观察的。该表的排列方式与表$3.2$中真实的捕获-再捕获数据相同。链接错误“扰乱”了表$3.2$中的数据，因此$n^*_{ijk}$​可能与$n_{ijk}$​不同，除了列表总数,$n_{1++}​，n_{+1+}$​和$n_{++1}$​。设$n$为所有观察到的不同单元的数目，也假设不受联动误差的影响。\
$\quad\quad$$Fienberg$和$Ding$$[23]$提出了对数线性模型的修正，该模型考虑了从真实构型$n$到已观测构型的可能转变，只考虑了缺失的环节。他们假设:\
$(i)$联动过程中无错误匹配;\
$(ii)$一个过渡最多只能向下走一层;\
$(iii)$保持原始状态(没有遗漏错误)的概率等于$\alpha$和跃迁到任何其他可能状态的概率等于$(1−\alpha)/(m−1)$，其中m是所有可能跃迁到且允许跃迁的可能状态的数目。

例如，在所有三个列表$(111)$中真实记录的个体可以以相同的概率$(1−\alpha)/3$产生以下模式{$(110)，(001)$}或{$(101)，(010)$}或{$(011)，(100)$}。\
$\quad\quad$类似地，{$(110)，(001)$}可以被观察为{$(110)，(001)$}或{$(100)，(010)，(001)$}，以此类推。这个公式可以很容易地扩展到一般的$k$列表数据。允许的转换结构产生了一个方程，该方程将链接表的单元概率关系式$(\pi \times = M\pi)$与真实表的单元概率关系式$(\pi \times = M\pi)$联系起来，并乘以$N$，得到期望的单元数为$E(N \times | N) = Mn$。\
$\quad\quad$为了估计总体规模$N$, $Fienberg$和$Ding$$[23]$建议根据给定$N$的条件似然计算$\pi$的$MLE$，如第$3.4.1$节所述。由$[51]$可知，条件$mle$和无条件$mle$在合适的正则条件下都是一致的。然后得到$n000$和NN的$mle$，如$3.2$节中$[22]$所述。\
$\quad\quad$董事会和导师$[17]$提出了一个扩展，以允许虚假链接除了丢失匹配。此外，他们还采用了一种误差模型，考虑到第$3.3.1$节所述的三清单联系程序的拟议操作模型，其中清单$1$和清单$2$首先相连，然后与清单$3$相连。\
$\quad\quad$因此，设$1−\alpha_1$为第一个匹配失败的概率连杆，并假设错过一个匹配的概率在第二连杆与第一个连杆操作$1−\alpha_2$的结果无关。同理，设$\beta_1$​和$\beta_2$​为两个键的假连接概率，分别假设错误链接的概率不依赖于第一个操作的结果。区分链接的两个操作中的错误是由不同列表中不同的关键变量质量驱动的。\
$\quad\quad$需要再一次考虑$n_{111}$。当只允许缺少匹配时，可能的从真实匹配模式$(111)$到观察到的模式的转换如下:

{$(111)$} &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;概率$\alpha_1\alpha_2$
{$(110),(001)$} &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;概率$\alpha_1(1-\alpha_2)$
{$(101),(010)$}或者{$(100),(011)$} &emsp;&emsp;概率$(1-\alpha_1)\alpha_2/2$
{$(100),(010),(001)$} &emsp;&emsp;&emsp;&emsp;概率$(1-\alpha_1)(1-\alpha_2)$


将所有其他真实匹配模式相似地放在一起，表$3.9$给出了从表$3.2$中的真实数据到表$3.8$中的观测数据的转换矩阵。

**表3.9**
从真实模式到观察模式的转换矩阵，只有缺失的环节
| |$(111)$ | $(110)$ |$(101)$  |$(100)$ |$(011)$ |$(010)$ |$(001)$ |
| -------- | -------- | -------- |-------- |------- |------- |------- |------- |
| $(111)^*$ | $\alpha_1\alpha_2$ |  ||  |  |  |  |
| $(110)^*$|$\alpha_1(1-\alpha_2)$  | $\alpha_1$ |  |  |  |  |  |
| $(101)^*$ | $(1-\alpha_1)\alpha_2/2$ |  | $\alpha_2$ |  |  |  |  |
| $(100)^*$| $(1-\alpha_1)(2-\alpha_2)/2$ | $1-\alpha_1$ | $1-\alpha_2$ | $1$ |  |  |  |
| $(011)^*$ | $(1-\alpha_1)\alpha_2/2$ |  |  |  | $\alpha_2$ |  |  |
| $(010)^*$ | $(1-\alpha_1)(2-\alpha_2)/2$  |  $1-\alpha_1$|  |  |  | $1$ |  |
| $(001)^*$ | $1-\alpha_2$ |  | $1-\alpha_2$ |  |  $1-\alpha_2$|  |  $1$|

$\quad\quad$接下来，可以扩展转换矩阵以包括假链接误差(表$3.10$)。此外，在每个阶段，只要错过了一个真匹配，就不会出现一个假链接，因为当至少同时出现两个错误时，就会发生此事件，类似于第$3.4.1$节和第 $3.4.2$ 节中两个列表的情况。最后，正如第$3.3.2$节中已经提到的，请注意，在表$3.10$中，假链接率是使用分母$(N_1−n_{11})+(N_2−n_{11})$来评估的，即列表$1$或列表$2$中不匹配的记录的数量以及 $(n_{11}−n_{111})+(N_3−n_{111})$ ，其中 n_{11}n11 表示在第一个列表之后的新列表

**表3.10**
转换矩阵从真实模式到观察模式，缺失和错误的链接
| |$(111)$ | $(110)$ |$(101)$  |$(100)$ |$(011)$ |$(010)$ |$(001)$ |
| -------- | -------- | -------- |-------- |------- |------- |------- |------- |
| $(111)^*$ | $\alpha_1\alpha_2$ | $\alpha_1\beta_2$ |$\alpha_2\beta_1$| $\beta_1\beta_2$ | $\alpha_2\beta_1$ |  |  |
| $(110)^*$|$\alpha_1(1-\alpha_2)$  | $(\alpha_1)(1-\beta_2)$ | $\beta_1(1-\alpha_2)$ | $(\beta_1)(1-\beta_2)$ | $\beta_1(1-\alpha_2)$ |  |  |
| $(101)^*$ | $(1-\alpha_1)(\alpha_2)/2$ | $(1-\alpha_1)\beta_2/2$ | $(1-\beta_1)(\alpha_2)$ | $(1-\beta_1)(\beta_2)$ |  |  |  |
| $(100)^*$| $(1-\alpha_1)(2-\alpha_2)/2$ | $(1-\alpha_1)(1-\beta_2/2)$ | $(1-\beta_1)(1-\alpha_2)$ | $(1-\beta_1)(1-\beta_2)$ | $-\beta_1$ |  |  |
| $(011)^*$ | $(1-\alpha_1)(\alpha_2)/2$ | $(1-\alpha_1)\beta_2/2$ |  |  | $(1-\beta_1)\alpha_2$ |  |  |
| $(010)^*$ | $(1-\alpha_1)(2-\alpha_2)/2$  |  $(1-\alpha_1)(1-\beta_2/2)$| $-\beta_1$ | $-\beta_1$ | $(1-\beta_1)(1-\alpha_2)$ | $1$ |  |
| $(001)^*$ | $1-\alpha_2$ | $-\beta_2$ | $1-\alpha_2$ | $-\beta_2$ |  $1-\alpha_2$|  |  $1$|

