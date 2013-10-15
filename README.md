#uccn
首先要说明的是，本作品是从 [uc](https://github.com/satyr/uc)派生出来，主要是做了汉化处理而已。
uc 是可以让您在 chrome 窗口中运行任意本地脚本的 [Firefox](http://firefox.com) 扩展。
简单地说就是 [userChromeJS](http://userchromejs.mozdev.org/) + [subscriptoverlayloader.js](http://stashbox.org/26086/subscriptoverlayloader.js)。

###用法
在选项中(工具 -> uc)选择脚本“路径”和“深度”，以便根据它们的 meta 数据块自动加载。

* 如果是目录的话，其下的直至指定深度的所有 *\*.uc.{js,xul,css}* 文件都会被加载。
* 如果深度为 0，路径将会被忽略。
* 默认设置是一个单一的
  _<[UChrm](https://developer.mozilla.org/index.php?title=en/File_I%2F%2FO)>_
  这表示它加载meaning that it loads the *chrome* directory in your current profile
  as does subscriptoverlayloader. Note that *userChrome.js* isn't loaded.

###supported metadata
The syntax is roughly identical to [Greasemonkey's](http://wiki.greasespot.net/Metadata_Block).

* __@name__
  The script name.

* __@include__ / __@exclude__
  The URL onto which this script is/isn't loaded.
  * `*` are wildcards.
  * If prefixed with `~`, the rest is treated as regular expression pattern.
    ([example](http://gist.github.com/57590))

* __@require__
  Accepts a script URL and loads it beforehand.
  * The URL can be absolute or relative, but must be local.
  * Will not load the same script twice for a window.

* __@delay__
  The delay before overlay in milliseconds. XUL only.

* @(whatever)
  All other meta data are stored simply as text data.
  `UC` object defined in each window keeps them.

###improvements from userChromeJS + subscriptoverlayloader.js
* Lets you specify files/directories to load.
* Targets subwindows as well, such as about:config or the sidebar UIs.
* Reads meta data only when necessary--on startup or on script update.
* Regex in @include/@exclude.
* @require

###drawbacks
* Runs on Firefox 3.5+ only.
* Scamps workaround for <http://bugzil.la/330458>.
