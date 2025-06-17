
## 01.基本用法
使用Python+flask实现了一个示例

`app.py`
```python
from flask import Flask
from flask_graphql import GraphQLView
from schema import schema

app = Flask(__name__)

app.add_url_rule(
    '/graphql',
    view_func=GraphQLView.as_view(
        'graphql',
        schema=schema,
        graphiql=True  # 启用 GraphiQL 界面
    )
)

if __name__ == '__main__':
    app.run(debug=True) 
```


`schema.py`
```python
import graphene

# 定义数据模型
class Book(graphene.ObjectType):
    id = graphene.ID()
    title = graphene.String()
    author = graphene.String()
    published_year = graphene.Int()

# 示例数据
books = [
    Book(id=1, title="Python编程：从入门到实践", author="Eric Matthes", published_year=2016),
    Book(id=2, title="深入理解计算机系统", author="Randal E. Bryant", published_year=2016),
    Book(id=3, title="算法导论", author="Thomas H. Cormen", published_year=2009),
]

# 查询定义
class Query(graphene.ObjectType):
    # 获取所有书籍
    books = graphene.List(Book)
    
    # 根据ID获取单本书
    book = graphene.Field(Book, id=graphene.ID(required=True))
    
    # 根据作者获取书籍
    books_by_author = graphene.List(Book, author=graphene.String(required=True))

    def resolve_books(self, info):
        return books

    def resolve_book(self, info, id):
        for book in books:
            if book.id == int(id):
                return book
        return None

    def resolve_books_by_author(self, info, author):
        return [book for book in books if book.author == author]

# 创建 schema
schema = graphene.Schema(query=Query) 
```


## 02. 概念理解

### 后端定义原理

#### 1. 定义字段

在 Query 类中，books = graphene.List(Book) 这行代码定义了一个 GraphQL 查询字段，名字叫 books，类型是 Book 的列表。
也就是说，GraphQL 查询时可以通过 books 字段获取所有书籍。

#### 2. 解析器函数

`def resolve_books(self, info): return books `这段代码定义了 `books` 字段的解析器（resolver）。
Graphene 的约定是：如果你有一个字段叫 `books`，那么它会自动寻找名为 `resolve_books` 的方法来处理这个字段的查询请求。

#### 3. 工作流程

- 当客户端通过 GraphQL 查询 `books` 字段时，Graphene 会自动调用 `resolve_books` 方法。

- `resolve_books` 方法返回了上面定义的 `books` 列表（即所有书籍的数据）。

- 最终，客户端就能拿到所有书籍的信息。


### Query

- 后端（Query 类）定义了可以被查询的“数据类型”和“入口”。
- 前端（GraphQL 查询语句）决定了具体要这些类型中的哪些字段。