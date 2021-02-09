# fork from: https://github.com/xwb1989/sqlparser
# sqlparser
func Walk(level int, visit Visit, nodes ...SQLNode)// 修改点: 对 Walk 函数增加 level 参数
# 可以修改字段名
```golang
        selectObj := stmt.(*sqlparser.Select)
	tagPrev := "mytable."
	sqlparser.Walk(0, func(level int, node sqlparser.SQLNode) (kontinue bool, err error) {
		if col, ok := node.(*sqlparser.ColName); ok {
			oName := col.Name.GetV()
			if oName == "id" {
				col.Name.SetV("_id") // 把字段名 id 修改为 _id
			} else if tagPrev != "" {
				col.Name.SetV(tagPrev + oName)// 把字段名加上前缀
			}
		}
		return true, nil
	}, selectObj)
```

