
# selpg

# 说明
## 1. 命令格式  
```java
selpg [-s startPage] [-e endPage] [-l linePerPage | -f] [-d dest] input_file >output_file 2>error_file
   ```

## 2. 参数
   `-s`：startPage，后面接开始读取的页号   
    `-e`：endPage，后面接结束读取的页号  
    `-l`：后面跟行数，代表多少行分为一页  
    `-f`：该标志无参数，代表按照分页符’\f’ 分页，一般默认72行为一页  
    `-d`：“-dDestination”选项将选定的页直接发送至打印机，“Destination”应该是 lp 命令“-d”选项可接受的打印目的地名称  
   ` input_file`，`output_file 2`，`error_file`：输入文件、输出文件、错误信息文件的名字  
   
(-s和-e是必须的参数，其它为可选参数，-l和-f参数不可能同时出现）

# 设计

 1. 导入所需包
 ```java
 package main

import (

	"fmt"
	"flag"
	"os"
	"io"
	"bufio"
	"os/exec"

)
```

 2. 定义结构体
 ```java
 type selpg_args struct
{
	start_page int
	end_page int
	in_filename string
	page_len int
	page_type bool

	print_dest string
}
 ```
3. main函数
```java
func main(){
	var args selpg_args
	get(&args)
	process_args(&args)
	process_input(&args)
}
```
4. 实现各个函数的功能
```java
get(&args)	//初始化，定义结构体各个变量的值
process_args(&args)	//检查输入的命令是否合理有效
process_input(&args)	//处理输入的命令
```
# 运行使用
使用以下命令
```java
go install github.com/github-user/selpg
selpg [-s startPage] [-e endPage] [-l linePerPage | -f] [-d dest] input_file >output_file 2>error_file
```

