### dict

java의 map 형식은 python의 dict 데이터 타입으로 바꿔서 사용할 수 있다. 



type=map 을 사용하여 가져오면 object 형식으로 가져오게 된다. 

사용자가 입력한 대로 가져오기 위해 아래와 같이 lambda 식을 이용하여 map으로변환한다. 	

```python
parser.add_argument('dictparameter1', required=False, type=map, help=' cannot be blank')
parser.add_argument('dictparameter2', required=False, type = lambda v: {int(k): v for k, v in (x.split(':') for x in v.split(','))}, help='dictparameter cannot be blank')
```



RestURL GET 요청 샘플 

```
GET http://localhost:5000/test?dictparameter=0:Date,2:Amount,5:Payee,9:Memo
```



결과 

```
dictparameter1 :  <map object at 0x000001FD07565AC8>
dictparameter2 :  {0: 'Date', 2: 'Amount', 5: 'Payee', 9: 'Memo'}
```





### list

list 형식은 3가지 방식이 있다. 

`type=list`, `action='split'`방식은 string을 무조건 한글자로 파싱한다는 한계가 있다.

이둘의 차이점은 데이터를 가져올 때, `type=list`은 list 형이지만,  `action='split' `은 string을 쪼개는 것뿐, list형으로 변환되진 않는다. 

 만약 커스텀하게 쪼개면서, list형으로 바로 변환하고 싶다면 lamda 형식을 사용하면 된다. 



```python
parser.add_argument('requestparameter1', required=False, type=list, help=' cannot be blank')
parser.add_argument('requestparameter2', required=False, action='split', help=' cannot be blank')
parser.add_argument('requestparameter3', required=False, type=lambda s: [int(item) for item in s.split(',')], help=' cannot be blank')
```



RestURL GET 요청 샘플 


```
GET http://localhost:5000/test?requestparameter1=0123456&requestparameter2=0123456&requestparameter3=0,1,2,3,4,5,6
```



결과

```
requestparameter1 :  ['0', '1', '2', '3', '4', '5', '6']
requestparameter2 :  0123456
requestparameter3 :  [0, 1, 2, 3, 4, 5, 6]
```





