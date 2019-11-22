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

(unwords.reverse.words) input -> words함수에 input 전달 -> words함수 리턴값을 reverse함수에 전달 -> reverse함수의 리턴값을 unwords에 전달


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



### Haskell Main 함수 do 액션



```haskell
main = do
	putStrLn "Please enter your name"
	name <- getLine
	putStrLn ("Hello, " ++ name ++ ", how are you?")
```



```haskell
putStrLn :: String -> IO()
getLine :: IO String
```

putStrLn은 String을 입력받고 IO()를 리턴함.

getLine은 IO액션이고, 실행되면 String을 하나 반환함.

<- 은 액션의 결과값을 얻어올때 용이한 문법임. 각 액션의 결과를 변수에 넣는것이 가능(마지막은 X)

```haskell
doGuessing num = do
   putStrLn "Enter your guess:"
   guess <- getLine
   if (read guess) < num
     then do putStrLn "Too low!"
             doGuessing num
     else if (read guess) > num
            then do putStrLn "Too high!"
                    doGuessing num
            else putStrLn "You Win!"
```



### 재귀

##### Factorial 함수

```haskell
factorial 0 = 1
factorial n = n * factorial (n-1)
```

factorial 함수를 실행할때 parameter의 값이 0이면 1을 반환하고 0이아닌 다른 정수라면 

factorial n = n * factorial (n - 1)을 실행함.

위와 같은 하스켈의 문법을 패턴 매칭이라고함.

##### Power 함수

```haskell
power :: (Int,Int) -> Int
power(x,0) = 1
power(x,y) = x * power(x,y-1)
```



##### Length 함수

```haskell
length2 :: [a] -> Int
length2 [] = 0
length2 (x:xs) = 1 + length xs
```



##### list_append 함수

```haskell
list_append :: [a] -> [a] -> [a]
list_append [] ys = ys
list_append (x:xs) ys = x : xs ++ ys 
```



##### takeInt 함수

```haskell
takeInt :: Int -> [Int] -> [Int]
takeInt 0 (x:xs) = []
takeInt m (x:xs) = x : (takeInt (m-1) (xs))
```



##### dropInt 함수

```haskell
dropInt :: Int -> [Int] -> [Int]
dropInt 0 xs = xs
dropInt m (x:xs) = dropInt (m-1) xs
```



### 일반화 하기

```haskell
multiplyList :: Integer -> [Integer] -> [Integer]
multiplyList _ [] = []
multiplyList m (n:ns) = (m*n) : multiplyList m ns
```

패턴매칭을 할때  don`t care에 대해서 사용할 수 있음. 

어떤값이 와도 상관이 없을때  _ (Don`t care)을 사용해서 철저하게 무시해주는것이 좋음.



### 람다식

함수의 등식을 써서 정의하는 대신, 람디식을 써서 함수를 정의 할 수 있다.

람다식은 각각의 인자를 나타내는 패턴과, 인자로 결과를 어떻게 계산하는지 나타내는 몸체로 이루어지지만, 만들어진 함수에 이름을 붙이지는 않음

map과 함께 사용하면 다음과 같은 형태가 가능.

```haskell
map (\x -> x + 3)[0..n]

map (\(x,y) -> x * y)[(t1,q1),(t2,q2),(t3,q3)]

map (\xs -> 'c':xs) ["apples", "oranges", "mangos"]
```





### 리스트
