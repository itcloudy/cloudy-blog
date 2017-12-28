# goa安装

* 安装goa和goagen
<pre><code>
go get -u -v github.com/goadesign/goa/...
go install github.com/goadesign/goa
go install github.com/goadesign/goa/goagen
</code></pre>
* 测试是否安装成功，cmd下输入`goagen`,若出现下面的内容说明安装成功
<pre><code>
bottles/1The goagen tool generates artifacts from a goa service design package.

Each command supported by the tool produces a specific type of artifacts. For example
the "app" command generates the code that supports the service controllers.

The "bootstrap" command runs the "app", "main", "client" and "swagger" commands generating the
controllers supporting code and main skeleton code (if not already present) as well as a client
package and tool and the Swagger specification for the API.

Usage:
  goagen [command]

Available Commands:
  app         Generate application code
  bootstrap   Equivalent to running the "app", "main", "client" and "swagger" commands.
  client      Generate client package and tool
  commands    Lists all commands and flags in JSON
  controller  Generate controller scaffolding
  
  </code></pre>