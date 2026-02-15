<details><summary>0215</summary>

## Java 입문
| Codetree로 기본 Java 문법을 익혀보자.

### 1. 기본 출력

`System.out.print();` 함수 사용

```
public class Main {
  public static void main (String args[]) {
    System.out.print("Hello") ;
  }
}
```

### 1-1. `C++`은 어떨까?

1) `cout` 함수 사용 가능.
2) 이 때, 표준 함수들은 함수 앞에 `std::`를 붙여줘야 한다.
3) 상단에 `using namespace std;`를 선언하면 매번 적지 않아도 된다.
4) `cout` 함수는 `iostream`이라는 헤더를 코드 상단에 포함해줘야 사용 가능.
```
#include <iostream>
using namespace std;

int main() {
  cout << "World";
  return 0;
}
```

### 1-2. 세 언어의 출력 결과 비교

|언어|수행시간|메모리|
|---|---|---|
|Python|47ms|16MB|
|Java|89ms|9MB|
|C++|8ms|0MB|

세 언어 중 `C++`이 제일 빠르고 메모리도 적었다.


### 2. 특수문자를 포함한 출력

포함하고자 하는 특수 문자 앞에 `\` 작성하기

```
public class Main {
  public static void main(String args[]) {
    System.out.print("\"Hello\"");
  }
}
```

### 2-1. `C++`은 어떨까?

동일하게, 포함시키고자 하는 특수 문자 앞에 `\` 작성하기

```
#include <iostream>
using namespace std;

int main() {
  cout << "\"Hello\"";
  return 0;
}
```



### 3. 줄바꿈된 문장 2개 출력하기

`System.out.println()`는 기본으로 줄바꿈을 포함하고 있기 때문에, 출력하고자 하는 문장 두 개를 모두 작성하면 된다.

```
public class Main {
  public static void main(String args[]) {
    System.out.println("Hello World");
    System.out.println("Java is fun!");
  }
}
```

### 3-1. `C++`은 어떨까?

`cout << endl;` 은 기본적으로 한 줄이 띄어지게 한다.

```
#include <iostream>
using namespace std;

int main() {
  cout << "Hello";
  cout << endl;
  cout << "C++ is fun";

  return 0;
}
```

### 4. 숫자 연속으로 출력하기

`" "`를 그대로 활용할 수 있다.
혹은 연산자 `+`와 따옴표 `" "` 같이 활용 가능.

```
public class Main {
  public static void main(string args[]) {
    System.out.print("3 5");
  }
}


public class Main {
  public static void main(String args[]) {
    System.out.print(3 + " " + 5);
    }
}
```


### 4-1. `C++`은?

`" "`내에 공백으로 구분 가능,
혹은 `<<`를 여러 번 사용 가능.

```
#include <iostream>
using namespace std;

int main() {
  cout << "3 5";

  return 0;
}


#include <iostream>
using namespace std;

int main() {
  cout << 3 << " " << 5 ;

  return 0;
}
```

</details>