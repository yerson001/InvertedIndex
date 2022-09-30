# InvertedIndex

## Ejecutar INVERINDEX un nodo
## Eliminar o agregar workers

### 1. Eliminar los hosts
 sudo nvim /etc/hosts

### 2. Eliminar los workers
/usr/local/hadoop/etc/hadoop/workers

## Iniciar Hadoop

su - hadoop

start-dfs-sh

jps

## HDFS web UI

http://master:9870

## YARN

start-yarn.sh

 yarn node -list

## Hadoop Web UI(replace the hostname for you hadoop master host name)

http://master:8088/cluster

## RUN

export HADOOP_CLASSPATH=$(hadoop classpath)
echo $HADOOP_CLASSPATH

## hadoop mkdir

hadoop fs -mkdir /InverIndex
hadoop fs -mkdir /InverIndex/Input
### Revisa en UI web si se crearon los directorios

## upload data 

hadoop fs -put '/home/master/Desktop/InverIndex/Input_data/file01' /InverIndex/Input
hadoop fs -put '/home/master/Desktop/InverIndex/Input_data/file02' /InverIndex/Input

## Compilar JAVA

cd /home/master/Desktop/InverIndex
javac InvertedIndex.java -cp $(hadoop classpath) -d '/home/master/Desktop/InverIndex/tutorial_classes/' 
jar -cvf firstTutorial.jar -C tutorial_classes/ .

## Send .jar hadoop

hadoop jar '/home/master/Desktop/InverIndex/firstTutorial.jar' InvertedIndex /InverIndex/Input /InverIndex/Output


## ver los resultados

hadoop dfs -cat /InverIndex/Output/*
hadoop dfs -cat /InverIndex/input/file1.txt

## Eliminar mkdir output
hadoop fs -rmdir /inverindex/output
