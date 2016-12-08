# pipe [![Go Report Card](https://goreportcard.com/badge/github.com/yaronsumel/pipe)](https://goreportcard.com/report/github.com/yaronsumel/pipe)  [![GoDoc](https://godoc.org/github.com/yaronsumel/pipe?status.svg)](https://godoc.org/github.com/yaronsumel/pipe)
small utility for handling with stdin/stdout/stderr unix pipes

 Installation
```
go get -u github.com/yaronsumel/pipe
```
      
 Sync Usage
Read is Sync Action to get all pipe data fits in the predifened size
```
	data,err := pipe.Read(pipe.Stdin,1024)
	if err!=nil{
		//do something with the error
	}
  ```
  
      
 Async Usage
AyncRead will keep reading from the pipe and write it back to StdDataChannel. Don't forget to handle the errors.
```
	StdinChannel := make(pipe.StdDataChannel)
	go pipe.AsyncRead(pipe.Stdin, 1024, StdinChannel)
	for {
		select {
		case stdin := <-StdinChannel:
			if stdin.Err != nil {
				panic(stdin.Err)
			}
			fmt.Println(stdin.Data)
		}
	}
  ```
  
