# 无障碍测试

## 01 人工测试 <a href="#fmy0a" id="fmy0a"></a>

### 无障碍测试相关技能 <a href="#v1drj" id="v1drj"></a>

<mark style="background-color:blue;">测试方法</mark>

无障碍测试方法和执行步骤

无障碍的缺陷类型和判定方法



<mark style="background-color:blue;">屏幕阅读器操作</mark>

PC：NVDA, JAWS，争渡等

macOS/iOS：旁白

Android：Talkback



<mark style="background-color:blue;">障碍用户使用习惯</mark>

障碍用户浏览方式的理解和学习

障碍用户操作方式的理解和学习



<mark style="background-color:blue;">相关标准规范</mark>

了解无障碍测试，无障碍实现相关的标准和规范



### 无障碍测试方法 <a href="#ww6r3" id="ww6r3"></a>

元素的检测

* 焦点的检测,是否应该存在焦点,焦点的尺寸是否合适
* 标签朗读检测,内容是否恰当
* 类型和状态朗读检测,内容是否正确,实现方式是否恰当
* 操作检测,是否可以被执行,执行的方式是否合适
* 操作反馈,执行后的结果是否可被获知,方式是否合理

页面的检测

* 焦点的拆分是否合理
* 焦点扫动浏览顺序是否合理（一般从上到下，从左到右）
* 焦点扫动浏览的跳转是否正常
* 焦点的访问范围是否合理
* 页面的变化是否可被用户获知，方式是否合理（跳转应用之后，焦点应该也跟着到新的位置）

### 常见无障碍缺陷类型及判定 <a href="#ozg5j" id="ozg5j"></a>

<table data-header-hidden><thead><tr><th width="112"></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>缺陷名称<br></td><td>用户影响<br></td><td>检测方法<br></td><td>通过标准<br></td></tr><tr><td>无焦点<br></td><td>只有具有焦点的元素才可被读屏用户访问和交互，无焦点的元素将无法被用户操作和感知。</td><td>使用读屏手势访问非装饰性元素,观察该元素是否可被聚焦。</td><td>元素存在焦点，读屏手势可准确聚焦。</td></tr><tr><td>无标签<br></td><td>用户无法获知元素的含义及作用。</td><td>焦点聚焦至检测元素，观察屏幕阅读器朗读内容。</td><td>控件、图片等界面元素具有恰当的标签,标签内容能够准确、简洁地描述元素的功能或目的。</td></tr><tr><td>类型缺失<br></td><td>用户无法获知元素类型,无法判断如何操作及使用此元素。</td><td>焦点聚焦至检测元素。观察屏幕阅读器控件类型提示是否正确。</td><td>元素包含正确的类型信息。</td></tr><tr><td>状态缺失</td><td>用户无法获知元素当前所处状态,无法根据元素当前状态确定操作。</td><td>触发元素的不同状态,观察屏幕阅读器在每种状态下是否正确提示状态相关信息。</td><td>元素在各个状态下类型信息均设置正确。</td></tr><tr><td>操作无响应</td><td><p>用户无法与元素进行交互。</p><p><br></p></td><td>聚焦控件,根据控件的类型判断交互方式,使用屏幕阅读器操作手势与之交互,观察手势操作是否生效。</td><td>控件类型设置合理,操作方式与控件惯常交互一致,读屏模式下,手势操作有效。</td></tr></tbody></table>

## 02 工具测试 <a href="#gjn2s" id="gjn2s"></a>

### iOS端自动化测试 <a href="#zwtjx" id="zwtjx"></a>

<mark style="background-color:blue;">Accessibility Inspector</mark>

是Apple提供的一款无障碍检测工具，集成在Xcode的开发工具之中。

功能主要有如下三个：

* Inspection：显示信息属性(和值)、操作方法以及对象在可访问性层次结构中的位置
* Audit：一键检测并展示当前界面中存在的可访问性问题。检测的并部署读屏相关，更多是对比度、点击区域等内容
* Settings：快速修改系统设置项， 实时显示调整后的效果。eg反转色、颜色增强



### Android端自动化测试 <a href="#eua79" id="eua79"></a>

<mark style="background-color:blue;">Accessibility Scanner</mark>

使用无障碍功能扫描仪app可发现改进应用无障碍功能的方法，包括触摸目标大小、色彩对比度和内容标签等；也会提供改进建议。

使用方法：安装并同意相关权限→更改对比度和触摸目标的尺寸阈值→扫描录制内容



<mark style="background-color:blue;">LINT</mark>

Android Studio会显示有关无障碍功能问题的lint警告，并提供指向源代码中包含这些问题的位置的链接。



<mark style="background-color:blue;">Accessibility Test Framework for Android(ATF)</mark>

ATF是Google提供的一个用于自动检测无障碍功能的Java库，包含了一套检查无障碍功能的代码，可用于自动化测试。ATF是开源的，可以在GitHub上找到。

可以检查的问题：

* 非文本内容或控件是否设置标签
* 文本内容对比度
* 控件触摸大小
* 界面元素其他属性及测试无障碍服务(元素状态、元素类型等)



<mark style="background-color:blue;">ATF+Espresso</mark>

Espresso是一个谷歌力推的UI自动化测试框架。ATF可作为Espresso可选组件使用，允许利用现有的Espresso测试来评估应用程序的无障碍问题。

Espresso中可以通过从设置方法调用AccessibilityChecks.enable()方法来启用可访问性检查。通过添加这一行代码，可以测试UI的辅助功能，从而可以直接将辅助功能检查集成到测试套件中。

```java
//1.在gradle中添加依赖
androidTestImplementation 'androidx.test.espresso:espresso-
accessibility:3.3.0-alpha05'
//2.导入AccessibilityChecks
import androidx.test.espresso.accessibility.AccessibilityChecks
//3.调用AccessibilityChecks.enable()方法
companion object {
    @BeforeClass @JvmStatic
    fun enableAccessibilityChecks() {
        AccessbilityChecks.enable()
    }
}
```

调用AccessibilityChecks.enable()会返回一个AccessibilityValidator对象，可以用它来自定义测试中ATF的行为。

```java
companion object{
@BeforeClass  @JvmStatic
fun enableAccessibilityChecks() {
    AccessibilityChecks.enable()
        .setRunChecksFromRootView(true)//扩大可访问性检查的范围，从根节点开始访问
        .setSuppressingResultMatcher(
matchesCheckNames('is' ("TextContrastViewCheck")))//屏蔽无障碍的对比度问题不再接收反馈
    }
}
```

