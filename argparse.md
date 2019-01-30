# argparse — 命令行选项、参数、子命令解析器

使用argparse编写自定义的命令行工具。

---
## 使用详情+注释

```
import argparse
import sys

class Command(object):
    def __init__(self):
        # prog=sys.argv[0], description描述语, epilog结束语,
        # parent可继承其他parser, prefix 参数前缀默认为-
        # fromfile_prefix_chars 文件前缀
        self.parser = argparse.ArgumentParser(prog='', description='', epilog='', fromfile_prefix_chars='@')
        self.args = None

    def add_args(self):
        # Action
        self.parser.add_argument('--foo', action='store_const', const=42)
        self.parser.add_argument('--bar1', action='store_true')
        self.parser.add_argument('--bar2', action='store_false')
        self.parser.add_argument('--bar3', dest='types', action='append_const', const=str)
        self.parser.add_argument('--verbose', '-v', action='count')
        self.parser.add_argument('-vs', '--version', action='version', version='%(prog)s 0.1', help='show version of program and exit')
        # Nargs
        # N为常数，?为0或1 若无参数出现(--bar5)为defult，有为const, *为任意个, +为1个以上
        # ?后可以为文件, argparse.REMAINDER为可以保留参数选项
        self.parser.add_argument('--bar4', nargs=2)
        self.parser.add_argument('--bar5', nargs='?', const='c', default='d')
        self.parser.add_argument('--bar7', nargs='*')
        self.parser.add_argument('--bar8', nargs='+')
        self.parser.add_argument('--infile', nargs='?', type=argparse.FileType('r'), default=sys.stdin)
        self.parser.add_argument('--outfile', nargs='?', type=argparse.FileType('w'), default=sys.stdout)
        self.parser.add_argument('--bar9', nargs=argparse.REMAINDER)
        # type可以调用函数, 可以为int，str. open
        # choices必须在其范围写参数值, 可以为range也可以为list
        self.parser.add_argument('--bar10', type=int, choices=range(5, 10))
        # reuqired必须有参数值
        self.parser.add_argument('--bar11', required=True)
        # metavar取个别名, 可以为元组
        self.parser.add_argument('--bar12', metavar='YYY')
        self.parser.add_argument('--bar13', nargs=2, metavar=('bar', 'baz'))
        # dest:关键字参数dest为目标参数项,位置参数默认
        self.parser.add_argument('--bar14', dest='bar')
        # groups: 组选项,help中按组分类,也可创建分组
        # add_mutually_exclusive_group互斥参数选项，只能出现一个
        group = self.parser.add_argument_group('group')
        group.add_argument('--foo1', help= 'foo1 help')
        group.add_argument('--foo2', help= 'foo2 help')
        group1 = self.parser.add_argument_group('group1', 'group1 description')
        group1.add_argument('--foo3', help= 'foo3 help')
        group2 = self.parser.add_mutually_exclusive_group()
        group2.add_argument('--foo4', help= 'foo1 help')
        group2.add_argument('--foo5', help= 'foo2 help')

    def parser_func(self):
        # 设置和获取默认参数值,关键字参数使用
        self.parser.set_defaults()
        self.parser.get_defaults()
        

    def show(self):
        if len(sys.argv) == 1:
            # 无参显示usage
            self.parser.print_usage()
        else:
            self.parser.parse_args()

    def get_args(self):
        self.args = self.parser.parse_args()

def AP_func():
    ArgumentParser.print_usage()
    ArgumentParser.print_help()
    ArgumentParser.format_usage()
    ArgumentParser.format_help()
    # 有其参数显示器message
    ArgumentParser.format_exit(status=0,message='')
    # 无参数报错误信息
    ArgumentParser.format_help(message)

def command_init(command_object):
    command_object.add_args()
    command_object.show()
    command_object.get_args()
    return command_object

if __name__=='__main__':
    cmd = command_init(Command())
```

## 参考
- [argparse](https://docs.python.org/3/library/argparse.html)
- [Argparse Tutorial](https://docs.python.org/3/howto/argparse.html#id1)
