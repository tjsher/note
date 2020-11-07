#for j:= range jobs(是个管道)的特点
##11行
```go
package main

import (
	"fmt"
	"time"
)

func worker(id int, jobs <-chan int, results chan<- int){
	fmt.Println("in worker func", id)
	//即使jobs是空的，也会等传进数据再开始执行for循环
	for j:= range jobs{
		fmt.Printf("worker%d, start job %d\n", id, j)
		time.Sleep(time.Second)
		fmt.Printf("worker%d, end job %d\n", id, j)
		results <- j * 2
	}
}

func main() {
	jobs:= make(chan int, 100)
	results := make(chan int, 100)
	//创建大小为3的waterpool
	for w := 1; w <= 3; w++{
		go worker(w, jobs, results)
	}
	for j := 1; j <= 5; j++{
		fmt.Println("in j<=5")
		jobs <- j
	}
	close(jobs)
	for a := 1; a <= 5; a++{
		<- results
	}
}
```
``` go
//运行结果
in worker func 2
in worker func 1
in j<=5
in j<=5
in j<=5
in j<=5
in j<=5
in worker func 3
worker3, start job 3
worker1, start job 2
worker2, start job 1
worker3, end job 3
worker3, start job 4
worker2, end job 1
worker2, start job 5
worker1, end job 2
worker3, end job 4
worker2, end job 5
```
