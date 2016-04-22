---
title: "Simiki报错UnicodeDecodeError: ascii codec can t decode byte 0xe的解决方法"
date: 2016-04-22 13:46
---

今天使用`simiki`写wiki时，发现不能generate静态网页，会报如下错误：
```python
Traceback (most recent call last):
  File "/usr/local/bin/simiki", line 11, in <module>
    sys.exit(main())
  File "/usr/local/lib/python2.7/site-packages/simiki/cli.py", line 419, in main
    generator.generate()
  File "/usr/local/lib/python2.7/site-packages/simiki/cli.py", line 235, in generate
    self.generate_pages()
  File "/usr/local/lib/python2.7/site-packages/simiki/cli.py", line 284, in generate_pages
    files = [f for f in files if not f.startswith(".")]
UnicodeDecodeError: 'ascii' codec can't decode byte 0xe5 in position 0: ordinal not in range(128)
```
baidu后，使用如下方法解决了该异常:
1. 找到simiki的主程序：
```
~ which simiki
/usr/local/bin/simiki
```
打开`simiki`文件，内容如下：
```python
#!/usr/local/opt/python/bin/python2.7

# -*- coding: utf-8 -*-
import re
import sys

from simiki.cli import main

if __name__ == '__main__':
    sys.argv[0] = re.sub(r'(-script\.pyw|\.exe)?$', '', sys.argv[0])
    sys.exit(main())
```
修改为：
```python
#!/usr/local/opt/python/bin/python2.7
# -*- coding: utf-8 -*-
import re
import sys

from simiki.cli import main

reload(sys)
sys.setdefaultencoding('utf-8')

if __name__ == '__main__':
    sys.argv[0] = re.sub(r'(-script\.pyw|\.exe)?$', '', sys.argv[0])
    sys.exit(main())
```
