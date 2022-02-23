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
	
	Engine, err := xorm.NewEngine("dm", "dm://SYSDBA:Dameng2021bg@119.96.178.132:10236")
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
