
# Linux permissions

|Binary|Octal|String representation|Meaning|
|---|---|---|---|
|000|0(0+0+0)|- - -|no permission|
|001|1(0+0+1)|- - x|execute|
|010|2(0+2+0)|- w -|write|
|011|3(0+2+1)|- w r|write + execute|
|100|4(4+0+0)|r - -|read|
|101|5(4+0+1)|r - x|read + execute|
|110|6(4+2+0)|r w -|read + write|
|111|7(4+2+1)|r w x|read + write + execute|
