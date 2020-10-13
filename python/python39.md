# python3.9

## Dictionary merge and update operation
- merge operation : |
- update operation : |=

Order of dictionary is preserved after Python 3.7.


### Merge operation
```
>>> dongju = {'age':28}
>>> park = {'sex':'male'}
>>> dongju | park
{'age': 28, 'sex': 'male'}
>>> park | dongju
{'sex': 'male', 'age': 28}
```

### Update operation

When you converting a list to dictionary, even if there are duplicate data in the list, you can easily handle it with the update operator.

```
>>> book = [('PRML', 1), ('PRML', 2)]
>>> aligned = {}
>>> for k, v in book:
...   aligned |= {k: v}
...
>>> aligned
{'PRML': 2}
```


## Remove prefix and suffix of string

- Like other string manipulation methods, it returns the changed value without modifying the string itself.
- If there is no matching prefix or suffix, it returns the original string.

### removeprefix()

```
>>> name = 'dongjuPark'
>>> name.removeprefix('dongju')
'Park'
>>> name
'dongjuPark'
>>> name.removeprefix('song')
'dongjuPark'
```

### removesuffix()

```
>>> name = 'dongjuPark'
>>> name.removesuffix('Park')
'dongju'
>>> name
'dongjuPark'
>>> name.removesuffix('Song')
'dongjuPark'
```

## Added zoneinfo module supporting IANA time zone

```
>>> from zoneinfo import ZoneInfo
>>> from datetime import datetime
>>> dt = datetime(2020, 10, 5, 12, tzinfo=ZoneInfo("Asia/Seoul"))
>>> print(dt)
2020-10-05 12:00:00+09:00
>>> dt.tzname()
'KST'
```

## Reference
[파이썬 3.9 릴리스와 주요 변경 사항](https://www.44bits.io/ko/post/python-3-9-release-note-summary)