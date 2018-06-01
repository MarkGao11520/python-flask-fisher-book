# 2.1 定义参数，判断查询参数q是否是isbn号

```
@app.route("/search/<q>/<page>")
def search(q,page):
    """
    搜索书籍路由
    :param q: 关键字 OR isbn
    :param page: 页码
    """
    # isbn isbn13 由13个0-9在数字组成
    # isbn10 由10表0-9表数字组组成，中间可能包含' - '

    isbn_or_key = 'key'
    if len(q) == 13 and q.isdigit():
        isbn_or_key = 'isbn'
    short_q = q.replace('-', '')
    if '-' in q and len(short_q) == 10 and short_q.isdigit():
        isbn_or_key = 'isbn'
    pass
```
知识点：
- 字符串有一个函数```isdigit()```可以判断是否为数字
- in 关键字可以判断一个字符串是否在另一个字符串内
- 多个逻辑判断排列原则：1.大部分判断结果为假的条件应该放在前面；2.需要查询数据库的操作由于会消耗资源，应该尽量靠后