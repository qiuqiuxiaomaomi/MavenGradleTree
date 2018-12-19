# MavenTree
项目管理研究

<pre>
Maven
   Maven是一个项目构建和管理工具
   Pom.xml(Project object model)
       在执行task时，maven会去项目根目录下读取pom.xml获取需要的配置信息
       包含元素：
           1）groupId 项目创建组织的唯一标识符
           2) artifactId 项目基地址名
           3）version  项目版本
           5）dependencies 依赖，在dependency中添加具体依赖
           6）repositories 用来存储artifact(依赖文件)的的，一般都是某个仓库
</pre>


<pre>
依赖冲突解决：

      maven在依赖冲管理中有一下几个原则。
           1）依赖是使用Maven坐标来定位的，而Maven坐标主要由GAV（groupId, artifactId, version）构成。如果两个相同的依赖包，
              如果groupId, artifactId, version不同，那么maven也认为这两个是不同的。
           2）依赖会传递，A依赖了B，B依赖了C，那么A的依赖中就会出现B和C。
           3）Maven对同一个groupId, artifactId的冲突仲裁，不是以version越大越保留，而是依赖路径越短越优先，然后进行保留。
           5）依赖的scope会影响依赖的影响范围。

      解决方案

           但出现了冲突的时候，比如系统出现了NoSuchMethodError，LinkageError 很有可能是你系统中出现了依赖冲突。出现冲突以后，
           可以按以下的步骤执行

           1.确定出了问题的jar包名称。通常可以在eclipse中查找冲突的类有在哪些依赖包里面出现了。并确定实际要使用的是那个包，冲
             突的包有哪些。
           2.通过mvn dependency:tree  >  tree.txt 导出全部的依赖。
           3.在导出的依赖文件中，查找问题相关的jar。确定这些jar是如何被依赖进来的，是直接依赖的还是通过传递依赖引入的。
           4.找到相互冲突的并需要排除的依赖的顶级依赖,并分析冲突的原因，冲突的原因可能是以下几种：
           5.同一个jar包但groupId, artifactId不同，这种冲突只能通过设定依赖的<exclusions> 来进行排除需要的版本jar包依赖
             路径较长，这种冲突可以把想要版本的依赖直接什么在依赖中，这样路径就最短了优先级最高。
</pre>