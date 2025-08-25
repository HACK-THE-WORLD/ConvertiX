# ConvertiX

作者：key

## 项目介绍

`ConvertiX` 是一款基于 `Rust 语言` 编写的网络安全工具，它主要用于常用网络空间测绘平台语句之间互相转换。支持五大测绘平台：FOFA、QUAKE、HUNTER、ZOOMEYE、THREATBOOK。输入任意一个平台的搜索语句即可获得其余四个平台转换后的语句。

## 项目使用

常用命令如下，将你输入的语句和平台进行对应的填入即可转换。

```shell
# 最简单的方式
./ConvertiX -p fofa -q 搜索语句

# 从文件读取搜索语句转换
./ConvertiX -p fofa -q @file.txt

# 输出不同的格式
# 默认格式
./ConvertiX -p fofa -q @file.txt -f raw
# JSON格式
./ConvertiX -p fofa -q @file.txt -f json

# 保存到文件
./ConvertiX -p fofa -q @file.txt -f raw -o result.txt
```

通过`-h/--help`可以查看更详细的信息：

```shell
[Cyberspace Asset Mapping Platform Query Statement Conversion Tool]

Usage: ConvertiX [OPTIONS] --query <QUERY> --platform <PLATFORM>

Options:
  -c, --config <CONFIG>      Configuration file path [default: config.json]
  -q, --query <QUERY>        Query statement (use @filename to read from file)
  -p, --platform <PLATFORM>  Source platform of the query statement
  -f, --format <FORMAT>      Output format [default: raw] [possible values: raw, json]
  -o, --output <OUTPUT>      Output file path (optional, defaults to stdout)
  -h, --help                 Print help (see more with '--help')
  -V, --version              Print version
```

## 配置文件

项目包含一个标准的JSON配置文件 `config.json`，你可以根据需要修改或扩展，注意的是`operators`属于逻辑操作符，不允许增删改否则会出错。如果你想要支持更多平台，默认情况下也可以支持，在 `config.json` 中添加新平台的配置，在对应平台的 `fields` 配置中添加新的字段映射即可（字段映射要求每个平台都应有配置）。

```json
{
  "fofa": {
    "fields": {
      "ip": "ip",
      "port": "port",
      "body": "body"
    },
    "operators": {
      "equal": "=",
      "and": "&&",
      "or": "||",
      "not_equal": "!=",
      "left_paren": "(",
      "right_paren": ")"
    }
  }
}
```
