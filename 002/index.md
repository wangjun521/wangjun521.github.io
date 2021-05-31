# 键盘按键事件详解

- KeyDown 触发后，不一定触发 KeyUp，当 KeyDown 按下后，拖动鼠标，那么将不会触发 KeyUp 事件。
- KeyPress 主要用来捕获数字(注意：包括 Shift+数字的符号)、字母（注意：包括大小写）、小键盘等除了 F1-12、SHIFT、Alt、Ctrl、Insert、Home、PgUp、Delete、End、PgDn、ScrollLock 、Pause、NumLock、{菜单键}、{开始键}和方向键外的 ANSI 字符
- KeyDown 和 KeyUp 通常可以捕获键盘除了 PrScrn 所有按键(这里不讨论特殊键盘的特殊键）
- KeyPress 只能捕获单个字符
-  KeyDown 和 KeyUp 可以捕获组合键。
-  KeyPress 可以捕获单个字符的大小写
- KeyDown 和 KeyUp 对于单个字符捕获的 KeyValue 都是一个值，也就是不能判断单个字符的大小写。
- KeyPress 不区分小键盘和主键盘的数字字符。
- KeyDown 和 KeyUp 区分小键盘和主键盘的数字字符。
- 其中 PrScrn 按键 KeyPress、KeyDown 和 KeyUp 都不能捕获。
  在使用键盘的时候，通常会使用到 CTRL+SHIFT+ALT 类似的组合键功能。对于此，我们如何来判定？
-  通过 KeyUp 事件能够来处理（这里说明一下为什么不用 KeyDown，因为在判定 KeyDown 的时候，CTRL、SHIFT 和 ALT 属于一直按下状态，然后再加另外一个键是不能准确捕获组合键，所以使用 KeyDown 是不能准确判断出的，要通过 KeyUp 事件来判定 ）
