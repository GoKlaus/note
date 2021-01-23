[toc]

# docker方式

```shell
docker pull zookeeper kafka 
```





启动

```shell
docker run -it -v /mydir:/data -v /mylogdir:/datalog -e ZOO_MY_ID=1
```

