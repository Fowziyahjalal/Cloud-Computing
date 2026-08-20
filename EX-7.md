# Ex.No 07 – Install Hadoop Single Node Cluster and Run WordCount

## Aim
To install a Hadoop single-node cluster and run a simple application (WordCount).

## About Hadoop
Apache Hadoop is an open-source framework for distributed storage and processing of large data sets on clusters of commodity hardware. Core modules:
- **Hadoop Common** – shared libraries and utilities
- **HDFS** – distributed file system for high aggregate bandwidth
- **Hadoop YARN** – resource management for job scheduling
- **Hadoop MapReduce** – programming model for large-scale data processing

## Installation Steps

1. **Install Java** (prerequisite):
   ```bash
   sudo apt-get update
   sudo apt-get install openjdk-7-jdk
   sudo apt-get install openjdk-7-jre
   java -version
   ```

2. **Install SSH server**:
   ```bash
   su
   apt-get install openssh-server
   ```

3. **Generate SSH key**:
   ```bash
   ssh-keygen -t rsa -P "" -f ~/.ssh/id_rsa
   ```

4. **Enable passwordless SSH to localhost**:
   ```bash
   cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys
   ```

5. **Create Hadoop group and user**:
   ```bash
   sudo addgroup hadoop
   sudo adduser --ingroup hadoop hadoop
   ```

6. **Copy the Hadoop tarball** (`hadoop-2.7.0.tar.gz`) to your home directory.

7. **Extract it**:
   ```bash
   sudo tar -xzvf hadoop-2.7.0.tar.gz -C /usr/local/lib/
   ```

8. **Change ownership**:
   ```bash
   sudo chown -R hadoop:hadoop /usr/local/lib/hadoop-2.7.0
   ```

9. **Create HDFS directories**:
   ```bash
   sudo mkdir -p /var/lib/hadoop/hdfs/namenode
   sudo mkdir -p /var/lib/hadoop/hdfs/datanode
   sudo chown -R hadoop /var/lib/hadoop
   ```

10. **Locate Java**:
    ```bash
    readlink -f /usr/bin/java
    ```

11. **Edit `~/.bashrc`** and add:
    ```bash
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
    export HADOOP_INSTALL=/usr/local/lib/hadoop-2.7.0
    export PATH=$PATH:$HADOOP_INSTALL/bin
    export PATH=$PATH:$HADOOP_INSTALL/sbin
    export HADOOP_MAPRED_HOME=$HADOOP_INSTALL
    export HADOOP_COMMON_HOME=$HADOOP_INSTALL
    export HADOOP_HDFS_HOME=$HADOOP_INSTALL
    export YARN_HOME=$HADOOP_INSTALL
    export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_INSTALL/lib/native
    export HADOOP_OPTS="-Djava.library.path=$HADOOP_INSTALL/lib/native"
    ```

12. **Reload**:
    ```bash
    source ~/.bashrc
    ```

13. **Set `JAVA_HOME`** in `hadoop-env.sh` (`/usr/local/lib/hadoop-2.7.0/etc/hadoop/hadoop-env.sh`):
    ```bash
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
    ```

14. **Configure `core-site.xml`**:
    ```xml
    <configuration>
      <property>
        <name>fs.default.name</name>
        <value>hdfs://localhost:9000</value>
      </property>
    </configuration>
    ```

15. **Configure `yarn-site.xml`**:
    ```xml
    <configuration>
      <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
      </property>
      <property>
        <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
        <value>org.apache.hadoop.mapred.ShuffleHandler</value>
      </property>
    </configuration>
    ```

16. **Create and configure `mapred-site.xml`**:
    ```bash
    cp mapred-site.xml.template mapred-site.xml
    ```
    ```xml
    <configuration>
      <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
      </property>
    </configuration>
    ```

17. **Configure `hdfs-site.xml`**:
    ```xml
    <configuration>
      <property>
        <name>dfs.replication</name>
        <value>1</value>
      </property>
      <property>
        <name>dfs.namenode.name.dir</name>
        <value>file:/var/lib/hadoop/hdfs/namenode</value>
      </property>
      <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:/var/lib/hadoop/hdfs/datanode</value>
      </property>
    </configuration>
    ```

18. **Update `/etc/profile`**:
    ```bash
    JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
    PATH=$PATH:$JAVA_HOME/bin
    export JAVA_HOME
    export PATH
    source /etc/profile
    ```

19. **Format the namenode**:
    ```bash
    hdfs namenode -format
    ```

20. **Start HDFS and YARN** (as the `hadoop` user):
    ```bash
    start-dfs.sh
    start-yarn.sh
    jps
    ```
    Expected daemons: `SecondaryNameNode`, `ResourceManager`, `DataNode`, `NameNode`, `NodeManager`.

21. **Browse the NameNode web UI**: http://localhost:50070

## Running the WordCount MapReduce Application

`WordCount.java`:
```java
import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;

public class WordCount {

    public static class TokenizerMapper extends Mapper<Object, Text, Text, IntWritable> {
        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context) throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
                word.set(itr.nextToken());
                context.write(word, one);
            }
        }
    }

    public static class IntSumReducer extends Reducer<Text, IntWritable, Text, IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
                sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        Job job = Job.getInstance(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

**Set environment variables:**
```bash
export JAVA_HOME=/usr/java/default
export PATH=${JAVA_HOME}/bin:${PATH}
export HADOOP_CLASSPATH=${JAVA_HOME}/lib/tools.jar
```

**Compile:**
```bash
bin/hadoop com.sun.tools.javac.Main WordCount.java
jar cf wc.jar WordCount*.class
```

**Run:**
```bash
bin/hadoop jar wc.jar WordCount /user/joe/wordcount/input /user/joe/wordcount/output
```

**View output:**
```bash
bin/hadoop fs -cat /user/joe/wordcount/output/part-r-00000
```

Sample output:
```
Bye     1
Goodbye 1
Hadoop  2
Hello   2
World   2
```

## Result
A Hadoop single-node cluster was installed, and the WordCount MapReduce program was executed successfully.
