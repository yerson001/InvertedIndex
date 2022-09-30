# InvertedIndex
## Ejecutar INVERINDEX un nodo
## Eliminar o agregar workers

### 1. Eliminar los hosts
~~~
 sudo nvim /etc/hosts
~~~
### 2. Eliminar los workers
~~~
sudo nvim /usr/local/hadoop/etc/hadoop/workers
~~~

## Get sources
~~~
git clone https://github.com/yerson001/InvertedIndex.git

cd InverIndex

mkdir build
~~~
## Iniciar Hadoop
~~~
su - hadoop

start-dfs.sh

jps
~~~
## HDFS web UI
~~~
http://master:9870
~~~
## YARN
~~~
start-yarn.sh

yarn node -list
~~~
## Hadoop Web UI(replace the hostname for you hadoop master host name)
~~~
http://master:8088/cluster
~~~
## RUN importante
~~~
export HADOOP_CLASSPATH=$(hadoop classpath)
echo $HADOOP_CLASSPATH
~~~
## hadoop mkdir
~~~
hadoop fs -mkdir /pagerank
hadoop fs -mkdir /pagerank/Input
~~~
### Revisa en UI web si se crearon los directorios

## upload data 
~~~
hadoop fs -put '/home/master/Desktop/InverIndex/Input_data/file0001' /InverIndex/Input
hadoop fs -put '/home/master/Desktop/InverIndex/Input_data/file0002' /InverIndex/Input
~~~
## Compilar JAVA
~~~
cd /home/master/Desktop/InverIndex
javac InvertedIndex.java -cp $(hadoop classpath) -d '/home/master/Desktop/InverIndex/build/' 
jar -cvf app.jar -C build/ .
~~~
## Send .jar hadoop
~~~
hadoop jar '/home/master/Desktop/InverIndex/app.jar' InvertedIndex /pagerank/Input /pagerank/Output
~~~

## ver los resultados
~~~
hadoop dfs -cat /InverIndex/Output/*
hadoop dfs -cat /InverIndex/input/file1.txt
~~~
## Eliminar mkdir output
~~~
hadoop fs -rmdir /inverindex/output
hdfs dfs -rm -r /pagerank/Output
~~~

## Guardar resultados de hadoop en .txt
~~~
 hadoop dfs -cat /inverindex/Output/* > resultados.txt
~~~
