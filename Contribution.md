## How to run profiling 
1:Get clone of https://github.com/rcherin/testservice and run it separately.
2:Get postgres docker image 
 ``` docker pull renzocherin/postgres-and-test-data:v2 ```
3:Run docker ( make sure any other your local postgres software is running ... to use localhost)
``` docker run --name <something you like> -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d <Image Id> ```
4:Get clone of https://github.com/chrisbrown1111/quarkus-eei-test 
5:Install k6 ( use brew for mac user)
6:Make sure you have profiling
```
	go func() {
		log.Println(http.ListenAndServe("localhost:6060", nil))
	}()
```
7:Run testservice ( should be port 7070)
8:Run go app  ( should be port 8080)
9:Run k6 
```
k6 run <filename>.js
```
10: Run pprof command on separate terminal and set what you want to see( profile or heap or whatver)
default is 30s
```
go tool pprof http://localhost:6060/debug/pprof/profile
```