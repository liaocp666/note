## 移动文本

|命令|说明|示例|
|--|--|--|
|w|word, 移动光标至下一个单词||
|wb|word break, 移动光标至前一个单词||
|:number|跳转 number 行||
|number G|跳转至 number 行||
|0|移动到行首||
|$|移动到行尾||
|gg|移动到文件开头||
|G|移动到文件结尾||
|ctrl+o|返回到上一个位置||


## 翻页文本

|命令|说明|示例|
|--|--|--|
|ctrl+f|forward||
|ctrl+u|upward||

## 插入文本

|命令|说明|示例|
|--|--|--|
|a|append, 当前光标后面插入||
|A|append，行最后插入||
|i|insert，当前光标前面插入||
|I|insert，行最前插入||
|o|open a line，当前光标下一行插入||
|O|open a line，当前光标上一行插入||

## 删除文本

|命令|说明|示例|
|--|--|--|
|d|delete，删除文本||
|dw|delete word，删除一个词语||
|diw|delete inner word，删除不包含空格的词语||
|daw|delete around word, 删除包括空格的词语||
|dd|删除一行||
|ctrl+w|插入模式下，快速删除||

## 修改文本

|命令|说明|示例|
|--|--|--|
|c|chanage，修改||
|ciw|change inner word, 删除单词并进入插入模式||
|ct)|change to ) , 修改到右边括号||

## 查找文本

|命令|说明|示例|
|--|--|--|
|fs|found s，查找当前行第一个出现的 s ，使用 ; 查找下一个||
|/word|顺序查找 word 单词出现的地方||
|?word|逆序查找 word 单词出现的地方||

## 其它

|命令|说明|示例|
|--|--|--|
|u|undo，撤销操作||
