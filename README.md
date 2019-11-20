# SangYeoop-HaskellStudy
SangYeoop/HaskellStudy







## Haskell?

함수형 프로그래밍 언어 -> 여기서 말하는 함수는 C, C++, Java말하는 함수, 메서드와는 다른 수학적인 함수를 말하는것 같음.



#### 함수합성

고등학교 수학때 합성함수에대해 배워본적이 있을텐데 하스켈에서는 이것을 함수합성으로 표현할 수 있음.

```haskell
revWords :: String -> String
revWords input = (unwords.reverse.words) input
```

```haskell
words :: String -> [String]
```

```haskell
reverse :: [a] -> [a]
```

```haskell
unwords :: [String] -> String
```

words , reverse, unwords는 전부 하스켈에서 지원하는 함수로 타입은 위와같이 되어있음.

words함수는 문자열을 뛰어쓰기를 기준으로 문자로 나눔

reverse함수는 리스트의 순서를 뒤바꿈

unwords함수는 words함수의 반대로 작동



#### 다형성

하스켈에서도 다른 객체지향 프로그래밍에서처럼 다형성을 나타낼 수 있음. 

```haskell
reverse :: [a] -> [a]
```

[a] -> [a] 이 뜻은,

a형 리스트를 인자로 받고 a형 리스트를 리턴한다는 뜻임.

보통 하스켈에서 타입이라고 한다면  Int , Num, String, Char, List, Tuple 등 많은 타입이 존재함.

그리고 하스켈을 공부하면서 느낀건데 하스켈은 타입에 대해 굉장히 엄격한것 같음.

타입이 맞지 않다면 구문오류가 나는데 이것을 매우 많이 겪어봄. 

근데 타입 하나 하나에 맞게 함수를 짜야한다면 매우 비효율적이므로 다형성을 지원함.

여기서 a는 어떠한 타입도 될 수 있음.

그래서 위의 reverse함수는

```Haskell
reverse :: [Int] -> [Int]
```

```Haskell
reverse :: [Num] -> [Num]
```

```Haskell
reverse :: [Char] -> [Char]
```

위와같은 메서드들을 통합해놓은것과 같음.





#### 타입





 

 