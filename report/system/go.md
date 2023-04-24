# Golang 패키지 관리



이 드럽고 치사한 언어는 왜 하는가?

**재밌자나**



## 디랙토리 하나에 파일 단일 인 경우

쨌든 Golang에서 패키지 관리 하는 부분에서 파이썬과 JS처럼 진행해보았다.



```go
// main.go

package main

import (
	"fmt"
	"lib/sum"
)

func main() {
	fmt.Println("asdf")
	fmt.Println(sum.Sum(10, 10))
}

```

이 형태로 만들면 무ㅜㅜㅜㅜㅜㅜㅜㅜㅜㅜㅜㅜㅜㅜㅜㅜㅜㅜ조건 에러다.



왜냐면 얘내들은 패키지 관리를 씨게 하니깐.



Golang은 go.mod이라는 파일을 만들어서 패키지 관리를 한다.

파이썬, JS처럼 구현할수있는 시스템이 아니라 좀 어렵게 느껴졌긴했다.



내가 어찌저찌해서 구현한거는 아래와 같이 디랙토리와 코드를 볼수있다.

```
// 디랙토리 형식
.
├── READMD.md
├── go.mod
├── lib
│   ├── go.mod
│   └── test.go
└── main.go
```



아래와 같이 구현하게 되었다.

```go
// ./lib/test.go

package sum

func Sum(x int, y int) int {
	return x + y
}
```



main.go에서는 go.mod에서 설정한 라이브러리를 사용할수있게 지정한다.

```go
// ./main.go
package main

import (
	"fmt"
	"test_lib/sum"
)

func main() {
	fmt.Println("asdf")
	fmt.Println(sum.Sum(10, 10))
}
```



근데 그전에 go.mod는 어떻게 설정했냐고?

아래와 같이 구성하게 되었다.



```go
// ./lib/go.mod

module test_lib

go 1.20

require (
    test_lib/sum v0.0.1
)
```

이렇게 미리 패키지 네임에 대한 버전 지정과 네임 지정을 디랙토리마다 설정한다.



```go
// ./go.mod
module test_lib

go 1.20

require (
    test_lib/sum v0.0.1
)

replace (
    test_lib/sum v0.0.1 => ./lib
)
```

이렇게 파일 위치와 파일 버전을 설정하여 불러오게 한다.

원래는 git를 이용하여 소스코드를 불러오고 그렇게 설계되어있는점에서는 확실히 좋은건 맞다 
하지만 로컬에서 모듈 구현하고 불러오기할때는 어느정도 파이썬과 비교하면 개발속도가 느려지는건 맞다.



~~뭐 어쩌겠어 내가 언어 만들면 그만인데~~



## 디랙토리 하나에 파일 다수 인 경우

실습중





## 각 소스코드 디랙토리 마다 소스코드 두개인경우

실습중