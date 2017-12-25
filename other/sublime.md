# sublime 相关


## 开发插件(插入当前时间)
* Tools -> Developer -> New Plugin
* 在新的页面中默认会出现下面的内容
<pre><code>
import sublime
import sublime_plugin


class ExampleCommand(sublime_plugin.TextCommand):
	def run(self, edit):
		self.view.insert(edit, 0, "Hello, World!")
</code></pre>
* 编码
<pre><code>
import sublime
import sublime_plugin
import datetime


class AddCurrentTimeCommand(sublime_plugin.TextCommand):
	def run(self, edit):
		self.view.run_command("insert_snippet",
            {
                "contents": "%s" % datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
            }
        )

</code></pre>
* 保存，会自动保存到用户路径`C:\Users\admin\AppData\Roaming\Sublime Text 3\Packages\User`下，命名为`addCurrentTime.py`
* 设置调用Preference -> Key Bindings -> User ,内容如下：
<pre><code>
[
    {"keys": ["shift+alt+d"], "command": "add_current_time"}
]
</code></pre>
* 使用快捷 ：`shift+alt+d` 即可插入当前时间