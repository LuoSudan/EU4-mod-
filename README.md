# 1 简单分析
写了两个非常简单的决议

谈一谈我对于EU4写决议的理解。

我看，给EU4写mod，是在**分子层面**的作业。也就是说，原子层面的那些东西是管不到的，也是不需要管的。那么这就有个问题，界限在哪里？哪一边是分子，哪一边是原子？我看，这就体现在P社所说的“**作用域**”。所以：

**凡是属于P社所规定的“作用域”范围内的东西，都是分子层面的。凡是不属于的，都是不需要管的。**

所以，mod用到的语法，它的主语总是“作用域”的两个对象：国家和省份。所以，总是针对它们，总是围绕它们，总是对它们给予考察、判断和修正。这也和游戏游玩的方式是完全一致的：玩家只需要关注这两个层面的东西：国家、省份，游戏里面的所有东西也都能分为：属国家的，或者属省份的。

所以，就有两种写法，**把国家当主语**的写法（通常都是这个，所以常常省略主语），**把省份当主语**的写法。

## 1.1 把国家当主语

前者的例子，来看这个决议：
```
country_decisions_01 = {
  potential = {
    tag = MNG
    stability = 0
  }
  allow = { 
    owns_core_province = 2157 #惠州
  }
  effect = {
    2157 = {
      change_trade_goods = cloves
    }
  }
}
```

其中，“tag”、“stability”、“owns_core_province”，显然就是站在国家的视角来看的，是把国家作为主语，并且**省略**了这个主语的。用自然语言来说，就是：（玩家正在操控的国家的）tag=XXX；（玩家正在操控的国家的）稳定度=x；（玩家正在操控的国家的）拥有核心的省份的编号=xxx。但是括号里面的都省略了。

这里可以重复提一下，一个决议中的3个主要部分：条件的条件、条件、效果。（一般说来还有第4项，即AI对待这个决议的行为，但是我是娱乐玩家，写mod为了自娱自乐，哪管那么多）其中，条件的条件（即potential部分）指的是：需要满足哪些要求，这个决议才会呈现到游戏中可见的列表当中；条件（allow）指的是：要满足哪些要求，这个决议才能点；效果（effect）指的是：决议产生的效果是怎么样的。

# 1.2 把省份当主语

而把省份当做主语的写法，同样还是看上面这个例子，就要专门提到这个主语了：

```
2157 = {
  change_trade_goods = cloves
}
```

2157**就是**主语，它是一个具体的省份。用自然语言来看，就是2157这个省份要被赋予如下效果：改变贸易品，变为丁香。

一切的mod语句编写都是基于这样一种思维。这里也就不再赘言。

还有一件事情要谈谈，就是写决议这件事主要会涉及到的方面。我看有**3个**：一个descisions文件里面的**决议清单**；一个是common-event_modifiers文件里面的自己设计的**修正列表**；还有一个是localization里面的**本地化**文件。这三个东西是紧密联系起来的。决议提供机制，修正（可选）带来效果（当然你也可以直接用那套现成的），本地化提供中文。

# 2 总结

总结一下，记住这种思维方式：所写的代码要么作用于国家，要么作用于省份；决议-修正-本地化是写决议的三件套，少了哪套都不好。
