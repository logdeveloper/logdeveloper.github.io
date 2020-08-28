---
title: "[Python] python flask 간단 예제"
categories:
  - Python
last_modified_at: 2020-07-31T11:00:00+09:00
toc: true
toc_sticky: true
toc_label: "목차"
tags:
  - 
  - 
  - 
sidebar:
  nav: posts
---





## Flask 실습

### CODE

```python
from flask import Flask
from flask_restful import  reqparse, abort, Api, Resource

app = Flask(__name__)
api = Api(app)

ORDERS = {
    'order1' : {'coffee' : 'americano'},
    'order2': {'coffee': 'latte'},
    'order3': {'coffee': 'espresso'},
}


def abort_if_todo_doesnt_exist(order_id):
    if order_id not in ORDERS:
        abort(404, message = "STARBUCKS ORDER {} doesn't exist".format(order_id))

parser = reqparse.RequestParser()
parser.add_argument('coffee')

class Order(Resource):
    def get(self, order_id):
        abort_if_todo_doesnt_exist(order_id)
        return ORDERS[order_id]
    def delete(self, order_id):
        abort_if_todo_doesnt_exist(order_id)
        del ORDERS[order_id]
        return '', 204
    def put(self, order_id):
        args = parser.parse_args()
        coffee= {'coffee' : args['coffee']}
        ORDERS[order_id] = coffee
        return coffee, 201

class OrderList(Resource):
    def get(self):
        return ORDERS;

    def post(self):
        args = parser.parse_args()
        order_id = int(max(ORDERS.keys()).lstrip()) + 1
        order_id = 'order_id%i' % order_id
        ORDERS[order_id] = {'coffee' : args['coffee']}
        return ORDERS[order_id], 201

api.add_resource(OrderList, '/orderlist')
api.add_resource(Order, '/order/<order_id>')

if __name__ == '__main__':
    app.run(debug=True)
```







### URL TEST



#### 1) GET

```
GET http://127.0.0.1:5000/orderlist
```

![1596173738239](/assets/images/2020-07-31-python-flask-simple-example/1596173738239.png)



```
GET http://127.0.0.1:5000/order/order3
```

![1596173728749](/assets/images/2020-07-31-python-flask-simple-example/1596173728749.png)



#### 2) DELETE


```
DELETE http://127.0.0.1:5000/order/order2
```

![1596173710804](/assets/images/2020-07-31-python-flask-simple-example/1596173710804.png)



#### 2) PUT

```
PUT http://127.0.0.1:5000/order/order2?coffee=iceamericano
```

![1596174078408](/assets/images/2020-07-31-python-flask-simple-example/1596174078408.png)



UPDATE

```
PUT http://127.0.0.1:5000/order/order2?coffee=latte
```

![1596174260974](/assets/images/2020-07-31-python-flask-simple-example/1596174260974.png)