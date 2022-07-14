# dm-xorm
添加以后让xorm支持达梦数据库

# 引入方法
```go
package main

import (
	"fmt"
	_ "gitee.com/chunanyong/dm" // google's odbc driver
	"github.com/go-xorm/xorm"
	_ "github.com/sjm1327605995/dm-xorm"
	"xorm.io/core"
)

type Person struct {
	A string `xorm:"A"`
	B string `xorm:"B"`
	C string `xorm:"C"`
}

func main() {
	
	Engine, err := xorm.NewEngine("dm", "dm://SYSDBA:PASSWORD@IP:PORT")
	if err!=nil{
		fmt.Println(err)
		return
	}
	Engine.SetTableMapper(core.SameMapper{})
	Engine.ShowSQL(true)
	Engine.SetMaxOpenConns(5)
	Engine.SetMaxIdleConns(5)
	if err=Engine.Sync(new(Person));err!=nil{
  	fmt.Println(err)
		return
  }
}
```

###
代码存在的问题，达梦的没有json数据类型。利用xorm做数据库切换，注意json或者jsonb类型。xorm写法最好加上""，不然sql会被达梦解析成大写的。导致查询不到
达梦过长的字符串无法作为主键。
