---
title:  "[C#] Dictionary란"
excerpt: C# 에서 사용하는 Dictionary란

categories:
  - C Sharp
tags:
  - [C#, Dictionary, 연관 배열, 사전형]

toc: true
toc_sticky: true
 
date: 2022-12-10
last_modified_at: 2022-12-10
---

## 개요
Dictionary란? <br>

--- 
=> Key와 Value 세트로 다루는 연관 배열로 인덱스 번호 대신 Key라는 값을 이용하여 Value라는 값을 취득하는 형식입니다. (Key는 중복 사용 불가)<br>

List와 비슷하지만 다른점이라면 List는 인덱스 번호로 요소의 값을 취득하는데 비해<br>
Dictionary는 상기와 같이 Key값을 이용하여 Value를 취득하므로 숫자, 문자열을 키로 지정하여 세트의 값을 취득하여 사용할 수 있습니다.<br>
따라서 항목과 값이 세트 데이터로서 다루어질 필요가 있을 경우 Dictionary 형을 이용합니다.
<br><br>

## 예제
--- 

정의
3가지 방법이 있으며 아래와 같습니다.
``` C#
var 오브젝트명 = new Dictionary<Key데이터형, Value데이터형>();
``` 

``` C#
Dictionary<Key데이터형, Value데이터형> 오브젝트명 = new Dictionary<Key데이터형, Value데이터형>()
``` 

``` C#
// 초기화도 같이 하는 방법
var 오브젝트명 = new Dictionary<Key데이터형, Value데이터형>()
    {
        {Key0, Value0},
        {Key1, Value1}
    };
``` 

<br>

### 데이터 추가 및 Key로 Value를 출력
``` C#
using System;
using System.Collections.Generic;
namespace test
{
    class MainClass
    {
        public static void Main(string[] args)
        {
            var _dictionary = new Dictionary<int, string>();

            // input data to use Add
            _dictionary.Add(1, "Dog");
            _dictionary.Add(2, "Honey Badger");
            _dictionary.Add(3, "Cat");

            Console.WriteLine("Export Dictionary");
            foreach (KeyValuePair<int, string> _value in _dictionary)
            {
                Console.WriteLine("[{0} : {1}]", _value.Key, _value.Value);
            }
        }
    }
}
```

####  build result

```
Export Dictionary
[1 : Dog]
[2 : Honey Badger]
[3 : Cat]
```
<br>

### Key 또는 Value만 출력
``` C#
using System;
using System.Collections.Generic;
namespace test
{
    class MainClass
    {
        public static void Main(string[] args)
        {
            var _dictionary = new Dictionary<int, string>();

            // input data to use Add
            _dictionary.Add(1, "Dog");
            _dictionary.Add(2, "Honey Badger");
            _dictionary.Add(3, "Cat");

            // show only keys
            foreach (int _key in _dictionary.Keys)
            {
                Console.WriteLine("{0}", _key);
            }


            // show only values
            foreach (string _value in _dictionary.Values)
            {
                Console.WriteLine("{0}", _value);
            }
        }
    }
}
```

#### build result

```
1
2
3
Dog
Honey Badger
Cat
```
<br>

### Key 또는 Value를 검색
``` C#
using System;
using System.Collections.Generic;
namespace test
{
    class MainClass
    {
        public static void Main(string[] args)
        {
            var _dictionary = new Dictionary<int, string>();

            // input data to use Add
            _dictionary.Add(1, "Dog");
            _dictionary.Add(2, "Honey Badger");
            _dictionary.Add(3, "Cat");

            Console.WriteLine("searching Key");
            // searching key
            int _key = 1;
            if (_dictionary.ContainsKey(_key)) {
                Console.WriteLine("{0}is already using as key", _key);
            } else {
                Console.WriteLine("[{0}is not using as key", _key);
            }

            Console.WriteLine("searching Value");
            // searching Value
            string _value = "Dog";
            if (_dictionary.ContainsValue(_value))  {
                Console.WriteLine("{0} is already exist", _value);
            } else {
                Console.WriteLine("[{0} is not exist", _value);
            }
        }
    }
}
```

#### build result

```
searching Key
1is already using as key
searching Value
Dog is already exist
```
<br>



<br>
[Top](#){: .btn .btn--primary }{: .align-right}