
# dandanplay-filter

弹弹play客户端使用的弹幕云过滤规则。

## 说明

此仓库用来维护 [弹弹play播放器](http://www.dandanplay.com) 中所使用的“云过滤”规则。每当仓库内容（包含过滤规则的 *.txt 文件）更新后，将通过 `build.ps1` 脚本将内容整合为一个 xml 文件，更新到服务器端，之后推送给所有弹弹play用户。

## 文件格式说明

所有屏蔽词将按照分类写入对应的 .txt 文件中，每行一个规则，使用`\n`换行。

规则文本使用正则表达式形式，所以支持 `.*?[]\w\s` 之类的符号。但由于之后所有屏蔽词会合并在一起，所以规则中不允许出现 `|` 字符。如果有这类需要，请将其分成不同的规则。

## 屏蔽原则

### 只处理与番剧相关的屏蔽词

由于弹弹play目前只包含番剧相关的弹幕库（动画、日剧等），此列表将只会处理与番剧相关的屏蔽词。对于其他分类的视频弹幕（例如B站游戏区、生活区）包含的梗将不会处理。

例如，下面的弹幕内容虽然影响观看，但由于几乎不在番剧中出现，所以不做屏蔽处理：

- 交出封面
- 失踪人口、关注列表
- 中医、西医
- 各种明星名字

### 屏蔽与视频内容无关的弹幕

“屏蔽与视频内容无关的弹幕”是判断某类弹幕内容是否应该屏蔽的最主要依据。如果弹幕内容和视频有关，不论其是否令某些人产生反感，弹弹play默认不会做屏蔽处理。反之，某些弹幕看起来活跃了弹幕气氛，但其与视频内容无关，弹弹play将会屏蔽他们。

举例说明：

- 不文明用语将被屏蔽
- 前排、打卡、日期、姓名、地点、漂移、三倍速 等内容因为与视频内容无关，将被屏蔽
- A站、B站、评论区、码率 等与特定平台相关的弹幕，因为与视频内容无关，将被屏蔽
- 完结撒花、反复横跳 等词语虽然容易令人反感，但因为一般与视频内容相关，将不会被屏蔽
- "前面说xxx的，xxxx"、"刷xxx的，xxx" 因为是回复其他弹幕而不是讨论视频内容，即使其目的是维护弹幕环境或指正别人的错误，也将会被屏蔽。因为引战和刷屏弹幕很有可能已被屏蔽，所以不必保留此类版聊弹幕
- "前面说xxx的笑死" 一般是由于讨论当前画面场景而产生的，虽然与其他弹幕有关，但不会被屏蔽。请注意区分此条与上一条的区别。

### 适当扩大屏蔽范围

弹弹play支持加载多个站的弹幕源，在这种情况下，弹幕质量比弹幕数量更加重要。在编写屏蔽词时，如果某个词语能很大程度上解决低质量弹幕问题，即使存在误伤正常弹幕的行为，也应该把它加入列表中。

目前列表中存在几个类似的规则：

- `^.$` 屏蔽了所有只包含一个字的弹幕
- `卡` 屏蔽了所有包含“卡”字的弹幕
- `你们` 屏蔽了所有包含“你们”一词的弹幕

### 维护轻松友好的弹幕环境

除了上述规则，弹弹play也将有意识维护弹幕环境的整体氛围，保证番剧观众尤其是新观众的良好观感，所以下面类型的弹幕也将被屏蔽：

- 剧透
- 讨厌某个角色（每个人对角色喜好不同）
- 认为剧情拖沓（每个人对剧情理解不同）
- 认为剧情尴尬或不好笑（每个人笑点不同）

目前由于番剧经常出现明显的画面崩坏情况，吐槽画面崩坏的弹幕将不会被屏蔽。

## 如何向此仓库贡献内容

请Fork后使用支持 `\n` 换行符的文本编辑器编辑 *.txt 文件。例如 [VS Code](https://code.visualstudio.com/) 和 [NotePad++](https://notepad-plus-plus.org/download/) 。请勿使用Windows记事本，它目前暂不支持`\n`换行符。

每份屏蔽词都分为简体中文和繁体中文两个版本。如果要进行修改，请将两边同步修改。[这里](http://ww.hao123.com/haoserver/jianfanzh.htm)是一个简单的在线简繁文字转换器。

修改完成后请提交 Pull Request 并附上增加或删除这些屏蔽词的原因。
