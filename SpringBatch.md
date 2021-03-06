### What is Spring Batch?
Spring Batch is an open source framework for batch processing. It is a lightweight, comprehensive solution designed to enable the development of robust batch applications. Spring Batch builds upon the POJO-based development approach of the Spring Framework. Spring Batch provides reusable functions that are essential in processing large volumes of records, including logging/tracing, transaction management, job processing statistics, job restart, skip, and resource management.

### What are features of Spring Batch?
The features of Spring Batch are as follows -
- Transaction management
- Chunk based processing
- Declarative I/O
- Start/Stop/Restart
- Retry/Skip
- Web based administration interface
- 
### What are disadvantages of Spring Batch?
The disadvantages of Spring Batch are as follows-
- Spring Batch code is complex. If one does not understand the framework then it can be difficult to understand the flow.
- The performance will not be good if not preperly implemented
- Exception handling can be complex.
- Logs for Spring Batch may not reflect/return the exception or issue we are looking for.

### What are use cases of Spring Batch?
- We can automate complex logic and efficiently process data without user interaction. 
- We can run these jobs daily
- Bulk data can be processed efficiently
- Data transformation and other operations can be performed in a transactional operation.

### What is ExecutionContext in Spring Batch?
An ExecutionContext is a set of key-value pairs containing information that is scoped to either StepExecution or JobExecution.Spring Batch persists the ExecutionContext , which helps in cases where you want to restart a batch run.
For example: When a fatal error has occurred, etc.

### How Spring Batch works?
![image](https://user-images.githubusercontent.com/100063114/158352383-8df13a8b-8344-4e31-9a23-f321745188ff.png)
- step - A Step that delegates to a Job to do its work. This is a great tool for managing dependencies between jobs, and also to modularise complex step logic into something that is testable in isolation. The job is executed with parameters that can be extracted from the step execution, hence this step can also be usefully used as the worker in a parallel or partitioned execution.
- ItemReader - Strategy interface for providing the data. Implementations are expected to be stateful and will be called multiple times for each batch, with each call to read() returning a different value and finally returning null when all input data is exhausted. Implementations need not be thread-safe and clients of a ItemReader need to be aware that this is the case. A richer interface (e.g. with a look ahead or peek) is not feasible because we need to support transactions in an asynchronous batch.
- ItemProcessor - Interface for item transformation. Given an item as input, this interface provides an extension point which allows for the application of business logic in an item oriented processing scenario. It should be noted that while it's possible to return a different type than the one provided, it's not strictly necessary. Furthermore, returning null indicates that the item should not be continued to be processed.
- ItemStreamWriter - Basic interface for generic output operations. Class implementing this interface will be responsible for serializing objects as necessary. Generally, it is responsibility of implementing class to decide which technology to use for mapping and how it should be configured. The write method is responsible for making sure that any internal buffers are flushed. If a transaction is active it will also usually be necessary to discard the output on a subsequent rollback. The resource to which the writer is sending data should normally be able to handle this itself.

### Difference between Step, Chunk and Tasklet
A Step is a domain object that encapsulates an independent, sequential phase of a batch job and contains all of the information necessary to define and control the actual batch processing.

Steps can be processed in either of the following two ways.
- Chunk
- Tasklet

![image](https://user-images.githubusercontent.com/100063114/158352746-67c139b6-558c-4492-af2e-90944518e484.png)

### What is Job?
A Job is the batch process to be executed in a Spring Batch application without interruption from start to finish. This Job is further broken down into steps.
A Job is made up of many steps and each step is a READ-PROCESS-WRITE task or a single operation task (tasklet).

~~~
/**
     * A Job is made up of many steps and each step is
     *  a READ-PROCESS-WRITE task or a single operation task (tasklet).
      * @return job
     */
    @Bean
    public Job simpleJob() {
        return jobBuilderFactory.get("simpleJob")
                .incrementer(new RunIdIncrementer())
                .flow(step1())
                .end()
                .build();
    }
~~~
### Why to use "incrementer(new RunIdIncrementer())" while configuring Job?
Ans:
incrementer(new RunIdIncrementer())
You can notice while creating Job, we have used incrementer. Since jobs uses a database to maintain execution state, you'll need an incrementer in this job definition. After that, you create a list of each step (though this job has only one step). When the job is completed, the Java API generates a perfectly configured job.

### Q: What is RunIdIncrementer in Spring Batch?
Ans:
We cannot rerun a Job if a JobExecution for this job has been COMPLETED, according to the Spring Batch guidelines. Since it updates the job parameters internally, a RunIdIncrementer instance can be used to run the same job multiple times.


### What is Step in Job?
Ans:
Spring Batch Step is an independent part of a job. As per above Spring Batch structure diagram, each Step consist of an ItemReader, ItemProcessor (optional) and an ItemWriter. Note: A Job can have one or more steps.
~~~
/**
 * Step consist of an ItemReader, ItemProcessor and an ItemWriter.
 * @return step
 */
@Bean
public Step step1() {
    return stepBuilderFactory.get("step1")
       .<String, String> chunk(1)
       .reader(new MessageReader())
       .processor(new MessageProcessor())
       .writer(new MessageWriter())
       .build();
}
~~~
### What is ItemReader?
Ans:
An ItemReader reads data into a Spring Batch application from a particular source.
~~~
public class MessageReader implements ItemReader<String> {
    /**
     * It read the data from the given source
     *
     * @return String
     * @throws Exception
     */
    @Override
    public String read() throws Exception {

        //read and pass message to processor to process the message
        return ...;
    }
}
~~~

##What is ItemProcessor?
Ans:
After reading the input data using itemReader, ItemProcessor applies business logic on that input data and then writes to the file / database by using itemWriter.

public class MessageProcessor implements ItemProcessor<String, String> {
    /**
     * Read input data from itemReader, and then ItemProcessor applies the business logic here
     *
     * @param content
     * @return String
     * @throws Exception
     */
    @Override
    public String process(String content) throws Exception {
       // handle business logic here
    }
}

What is ItemWriter?
Ans:
ItemWriter writes data from the Spring Batch application to a particular destination.

public class MessageWriter implements ItemWriter<String> {
    /**
     * ItemWriter writes received data to destination.
     *
     * @param inputMessage
     * @throws Exception
     */
    @Override
    public void write(List<? extends String> inputMessage) throws Exception {
        // write data to destination eg to database MYSQL etc..
    }
}
