### Git flow (git工作流)
#### 01 - 首先，项目存在两个长期分支。

* 主分支master
    * Git主分支的名字，默认叫做Master。它是自动建立的，版本库初始化以后，默认就是在主分支在进行开发。

* 开发分支develop
    * 我们把开发用的分支，叫做Develop，这个分支可以用来生成代码的最新隔夜版本（nightly）。如果想正式对外发布，就在Master分支上，对Develop分支进行"合并"（merge）
        ```
        //切换到Master分支
        　　git checkout master
        
        //对Develop分支进行合并
        　　git merge --no-ff develop
        ```
![image](https://github.com/Alley23/images_sources/blob/master/images/01-merge.jpg)

> 前者用于存放对外发布的版本，任何时候在这个分支拿到的，都是稳定的分布版；后者用于日常开发，存放最新的开发版。


#### 02 -  其次，项目存在三种短期分支

* 功能分支（feature branch）
    * 它是为了开发某种特定功能，从Develop分支上面分出来的。开发完成后，要再并入Develop。
    * 功能分支的名字，可以采用feature-*的形式命名。
    ```
    //创建一个功能分支
    git checkout -b feature-x develop
    //开发完成后，将功能分支合并到develop分支
    git checkout develop 
    git merge --no-ff feature-x
    //删除feature分支
    git branch -d feature-x
    ```
![image](https://github.com/Alley23/images_sources/blob/master/images/02-feature.jpg)

* 预发分支（release branch）
    * 它是指发布正式版本之前（即合并到Master分支之前），我们可能需要有一个预发布的版本进行测试。
    * 预发布分支是从Develop分支上面分出来的，预发布结束以后，必须合并进Develop和Master分支
    * 它的命名，可以采用release-*的形式。
    ```
    //创建一个预发布分支
    git checkout -b release-1.2 develop
    //确认没有问题后，合并到master分支
    git checkout master
    git merge --no-ff release-1.2
    //对合并生成的新节点，做一个标签
    git tag -a 1.2
    //再合并到develop分支
    git checkout develop
    git merge --no-ff release-1.2
    //最后，删除预发布分支
    git branch -d release-1.2
    ```
![image](https://github.com/Alley23/images_sources/blob/master/images/03-release.jpg)

* 补丁分支（hotfix branch）
    * 最后一种是修补bug分支。软件正式发布以后，难免会出现bug。这时就需要创建一个分支，进行bug修补
    * 修补bug分支是从Master分支上面分出来的。修补结束以后，再合并进Master和Develop分支。
    * 它的命名，可以采用fixbug-*的形式。
    ```
    //创建一个修补bug分支
    git checkout -b fixbug-0.1 master
    //修补结束后，合并到master分支
    git checkout master
    git merge --no-ff fixbug-0.1
    git tag -a 0.1.1
    //再合并到develop分支
    git checkout develop
    git merge --no-ff fixbug-0.1
    //最后，删除"修补bug分支"
    git branch -d fixbug-0.1
    ```
![image](https://github.com/Alley23/images_sources/blob/master/images/04-bug.jpg)


> 一旦完成开发，它们就会被合并进develop或master，然后被删除



