# iOS无障碍组建、属性与实践

<figure><img src="../../.gitbook/assets/accessibility__d3k04fax5jyq_og.png" alt=""><figcaption><p>苹果官网辅助功能页面的图片，让苹果专属于你。“专属于你”被选中，提示可以朗读</p></figcaption></figure>

在无障碍上，苹果是我和众多视障朋友最喜欢的厂商了，是它引领了智能手机的配置无障碍功能，每年的残障相关节日也有足够的人文关怀。由于出色的旁白功能，我认识的大部分视障者都在用苹果手机。

iOS具备的无障碍功能已经在第三篇讲了，这里讲技术实践。其他网站如CSDN、阿里云社区也有移动端开发的帖子，技术方案更加详细，进一步学习的可以去找它们。

{% content-ref url="chang-jian-de-wu-zhang-ai-fu-zhu-ji-shu.md" %}
[chang-jian-de-wu-zhang-ai-fu-zhu-ji-shu.md](chang-jian-de-wu-zhang-ai-fu-zhu-ji-shu.md)
{% endcontent-ref %}



## 01 焦点 <a href="#mili9" id="mili9"></a>

焦点是开启旁白功能后，点击屏幕聚焦后会出现黑色的边框。旁白会播报焦点内的元素信息。

焦点通过isAccessibilityElement属性控制，设置为NO时元素不可被聚焦。



## 02 朗读 <a href="#jvtdk" id="jvtdk"></a>

### 朗读相关属性 <a href="#cae3e" id="cae3e"></a>

_accessibilityLabel_

标签，一个简短的本地化单词或短语，用于简洁地描述控件或视图，但不去标识元素的类型。



_accessibilityValue_

元素当前的值。



_accessibilityTraits_

Trait主要用于说明元素的类型（特征)与状态。例如UIAccessibilityTraitButton可以用来描述一个「按钮」的类型，UIAccessibilityTraitSelected可以用来描述「选中」的状态。这两个Trait组合起来可以共同描述一个处于选中状态的按钮。

和accessibilityLabel不同，accessibilityTraits的值为开发者预先定义好的常量，设置完成后，常量所对应的描述文本可被旁白读出。示例代码：xxx.accessibilityTraits=UIAccessibilityTraitAdjustable



_accessibilityHint_

用一个手指上下轻扫来调整值。一个简短的本地化短语，描述对元素可执行的操作及操作的结果。例如“轻点两下以打开"或“用一个手指上下轻扫来调整值”。

此部分信息通常无需额外设置。在设置恰当的accessibilityTraits属性后，通常会提供恰当的accessibilityHint 信息。

<figure><img src="../../.gitbook/assets/640 (20).png" alt=""><figcaption></figcaption></figure>



### 适配技巧 <a href="#ywzu4" id="ywzu4"></a>

* 继承原生组件或使用无障碍状态良好的组件库，大部分组件已经提供了相关的属性内容，可以节省大量的适配工作。
* 当不清楚某个元素的应该如何设置时,可以观察系统自带应用，如“设置”、“应用商店"内近似元素的朗读，使用accessibility lnspector检查属性是如何设置的。
* 文本内容的设置应保持简洁，清晰，避免详细冗长的说明，这会很大程度影响用户获取信息的效率。
* 每个属性都有各自的作用，只有每个属性都正确设置时，元素才是可访问的，遵照属性规范的用法构建代码，避免将所有朗读内容都写入标签中的做法。



## 03 手势操作 <a href="#ef9f9" id="ef9f9"></a>

### 单指点两下 <a href="#nqnqw" id="nqnqw"></a>

等于非读屏模式的点击手势。



适配要点：

1.通常情况下无需设置，轻点两下事件会被原有的Tap手势事件捕获并响应。

2.确保元素的类型即accessibilityTraits属性正确设置，通常为按钮或者特殊类型的按钮，此时旁白会提示用户元素可点击。若操作后元素状态发生变化，也需要调整相关的Trait。



API参考

类型描述accessibilityTraits

用户执行操作手势时调用 (BOOL)accessibilityActivate



### 单指上下扫动 <a href="#mucet" id="mucet"></a>

通常用于值的调整，比如页面控制器、滑块。



适配要点：

1.确保元素的类型即accessibilityTraits属性正确设置，元素的类型需要设置为UIAccessibilityTraitAdjustable ，旁白会提示用户用一个手指上下轻扫调整值。

2.调整后的值在accessibilityValue中反馈给用户。

3.向上扫动代表值的增加，向下扫动代表值的减少。



API参考

类型 UIAccessibilityAdjustable

值 (String\*)accessililityValue

向上扫动 (void)accessibilityIncrement

向下扫动 (void)accessibilityDecrement



### 三指滑动 <a href="#jmtah" id="jmtah"></a>

通常用于滚动视图，tableView纵向的, collectionView横向的, feed流。此时旁白除了告知我们当前焦点聚焦的元素的信息，还会提示所在的页面是第几页、一共多少页。



适配要点：

1.accessibilityScroll方法被调用的过程中会传递进来用户滑动的方向，需要根据方向的不同做出不同的响应。

2.UITableView , UICollectionview已经实现了此方法，开发者无需额外处理。

3.向上/右滑动为向后，向下/左滑动为向前。

4.用播报通知的方法把滚动后的页面状态传递给用户。



API参考

调用(BOOL)accessibilityScroll:(UIAccessibilityScrollDirection)direction



### 适配技巧 <a href="#adpzx" id="adpzx"></a>

* 继承原生组件或使用、开发无障碍状态良好的组件库,大部分组件已经支持了上述的旁白手势，并不需要额外进行适配。
* 设置手势时不要忽略了对accessibilityTraits属性的设置，它会提示用户该如何与元素进行交互。
* 操作造成的变化，也需要以恰当的方式传递给用户。
* 遵照手势的使用规范进行设计，避免一些自定义手势，或改变原有手势的惯常行为，这会给用户增加额外的使用成本。



## 04 转子 <a href="#q04gk" id="q04gk"></a>

转子是旁白的一项功能，提供一种可以用于调整旁白的工作方式的方法，比如调节语言或语速、切换浏览方式等。转子的示意图如下图。

<figure><img src="../../.gitbook/assets/640 (19).png" alt=""><figcaption></figcaption></figure>

转子的切换可以在开启旁白后，单指向上滑动，单指向下滑动，此时屏幕中间就会出现一个黑色的功能面板，再次执行上述操作，就可以在选项间切换。(通过改变双指的滑动方向，可以实现顺逆时针的切换)也可以切换到某项功能后，通过上下扫动的手势进行使用。



### 自定义操作 <a href="#vnddg" id="vnddg"></a>

转子里有一项功能叫“操作”，可以在那自定义功能。



适配方法

1.根据需要创建自定义操作，每个操作我们需要传入一个名称，即旁白朗读的操作名称，和选择器对应调用后执行的方法。

2.将自定义操作添加至元素accessibilityCustomActions数组中。



代码参考

```java
//创建自定义的action
UIAccessibilityCustomAction *action1 =[[UIAccessibilityCustomAction alloc]
initWithName:@"" target: self selector: @selector()];

//将action加入元素的action列表中
self.accessibilityCustomActions = @[action1,action2 ...];
```



### 自定义内容 <a href="#fc44w" id="fc44w"></a>

在进行feed流（比如好友动态）的浏览时，通常会从先简单阅读标题概览，对于不感兴趣的内容往往会直接跳过。我们可以将元素的关键信息和非关键信息区分开，默认提供给用户关键信息，当用户切换到转子的自定义内容模式时，可以通过上下扫动来获知更多信息，当用户不感兴趣时，可以扫动浏览切换到下一条信息。



代码参考

```java
class FeedTableViewCell:UITableViewCell, AXCustomContentProvider{
    override var accessibilityLabel: String? (
        get{
        return name.text! +""+ title.text!
        set {}
    }

    var accessibilityCustomContent: [AXCustomContent]! {
        get{
        let descriptions= AXCustomContent(label:"描述"，value: descriptions.text!)
        let date = AXCustomContent(label:"时间", date:.text!)
        let location = AXCustomContent (label:"位置" value: location.text!)
        return (descriptions, date, location]
                }

    set{}
}
```

### 适配技巧 <a href="#lqsy7" id="lqsy7"></a>

* 元素包含多种交互方式时，使用转子是对用户很友好的一种方案，操作简单，不会影响用户的访问效率，同时也会很大程度避免误操作。
* 对于元素值的调整，优先考虑上下扫动这一手势，而不是适配转子的自定义操作。不要滥用转子的自定义操作功能。
* 使用自定义内容有2点需要注意:1.考虑低版本适配方案，此功能仅支持iOS14以上设备。2.由于功能较新，适配产品较少，也存在用户不熟知的情况。
* 把核心的信息放在朗读序列的最前面，也可以解决内容获取的效率问题，用户获取到核心信息后，可以自行决定是否跳过。这也是目前被广泛使用的方式。



## 05 页面设计 <a href="#sjpaj" id="sjpaj"></a>

### 焦点的有序 <a href="#azsqh" id="azsqh"></a>

视障用户在使用旁白时，经常需要通过扫动的方式依次遍历界面展示的内容，开发者需要确保这些信息是以连贯、结构化的形式组织起来，减少理解障碍。



适配要点

1.打包子视图：这样焦点在访问到这个视图时，只有完成视图内所有子视图的访问之后才可以访问其它视图。

2.调整访问顺序：调整视图内子元素返回顺序，旁白就会按照指定的顺序返回。



代码参考

```java
//方法1
containerView.shouldGroupAccessibilityChildren= YES;
//方法2
containerView.accessibilityElements =[subview1 , subview2];
```



### 焦点的合并 <a href="#r7bsm" id="r7bsm"></a>

并不需要给每个元素都设置单独的焦点，有些可以合并起来。

代码参考

```java
//如果元素在一个容器内，可以隐藏元素焦点，只展示容器作为一个独立焦点
containerView.isaccessibilityElement = YES;
containerView.accessibilityLabel= abel.text;

//或者，不考虑层级关系对两个元素进行融合
UIAccessibilityElement "mergeView=[[UIAccessibilityElement alloc] initWithAccessibilityContainer: containerView]; mergeView.accessibilityLabel= textView.text;
mergeElement.accessibilityFrameInContainerSpace = CGRectUnion (textView.frame, imageView.frame);
containerView.accessibilityElements = @[mergeView];
```



### 焦点的落点 <a href="#dmw6e" id="dmw6e"></a>

进入一个新页面or当前页面发生刷新时，可以调整焦点的落点到想要聚焦的元素。



适配要点

在页面发生变化时，发送一条通知告知旁白页面发生了变化，同时传入焦点的预期落点。



代码参考

```java
//arguement为预期落点
UIAccessibilityPostNotification (UIAccessibilityScreenChangedNotification, arguement);
```



### 底层元素 <a href="#qdq3a" id="qdq3a"></a>

界面上的弹窗，或者类似视图出现时，为了方便用户更好理解和操作，我们希望把除弹窗外元素的焦点都进行隐藏，以便用户更好的理解和操作。



适配要点

1.弹窗的适配存在较多的情况，在适配的过程中，我们需要先检查弹窗当前的情况，再根据不同的实现方式调整适配的方案。

2.比较常见的一种解决是，即弹窗的视图层和内容的视图层为兄弟关系。



代码参考

```java
//屏蔽兄弟视图层级的焦点
alert.accessibilityViewlsModal = YES;

//刷新页面并移动焦点至预期落点
UIAccessibilityPostNotification (UIAccessibilityScreenChangedNotification, alert.accessibilityElements.firstObject);
```



### 提示信息 <a href="#uhpfa" id="uhpfa"></a>

短暂停留在页面的提示信息。可以在信息出现时给用户发送一条通知，告知用户提示的内容。



适配要点

1.发送一条朗读的通知给旁白，提供需要朗读的内容。

2.实际使用中,这条通知存在被其它内容的朗读打断的问题，推荐在这里使用GCD延迟播报。



代码参考

```java
dispatch_after (dispatch_time (DISPATCH_TIME_NOW, (int64_t)([O.1* NSEC_PER_SEC)), dispatch_get_main_queue()，
^{UIAccessibilityPostNotification(UIAccessibilityAnnouncementNotification, announcementString);
});
```

