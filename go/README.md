# 介绍
go：替代C的最佳人选
1. 和C融合
1. 面向对象
1. 网络并发协程
1. 包管理体系，能出来生态，C++很尴尬

# 资料
* https://chai2010.cn/advanced-go-programming-book/
* https://juejin.im/post/6844904008893595661

# 使用
go run test.go
```
// 多态，Web服务
package main

import (
    "fmt"
    "log"
    "net/http"
    "time"
)

// 正方形
type Square struct {
	side float32
}

// 长方形
type Rectangle struct {
	length, width float32
}

// 接口 Shaper
type Shaper interface {
	Area() float32
}

// 计算正方形的面积
func (sq *Square) Area() float32 {
	return sq.side * sq.side
}

// 计算长方形的面积
func (r *Rectangle) Area() float32 {
	return r.length * r.width
}

func main() {
	fmt.Println("Hello, World!")
	r := &Rectangle{10, 2}
	q := &Square{10}

	// 创建一个 Shaper 类型的数组
	shapes := []Shaper{r, q}
	// 迭代数组上的每一个元素并调用 Area() 方法
	for n, _ := range shapes {
		fmt.Println("图形数据: ", shapes[n])
		fmt.Println("它的面积是: ", shapes[n].Area())
	}

	fmt.Println("Please visit http://127.0.0.1:12345/")
    http.HandleFunc("/", func(w http.ResponseWriter, req *http.Request) {
        s := fmt.Sprintf("你好, 世界! -- Time: %s", time.Now().String())
        fmt.Fprintf(w, "%v\n", s)
        log.Printf("%v\n", s)
    })
    if err := http.ListenAndServe(":12345", nil); err != nil {
        log.Fatal("ListenAndServe: ", err)
    }
}
```
