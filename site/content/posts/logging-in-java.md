---
title: Logging in Java
weight: 7
authors:
  - rmhari
tags:
  - KJSKj
authorimage: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSOd256TcC6vcaQ99TYzoP0pBbch9_Q-bbrmw&usqp=CAU'
---


Logging Greatness:

For many years, logs have been an essential part of troubleshooting application and infrastructure performance. They help provide visibility into how our applications are running on each of the various infrastructure components.

Log data contains information such as out of memory exception or hard disk errors. This is very helpful information that will help us identify the “why” behind a problem either that a user has brought to our attention or that we have uncovered.

But their sheer volume can limit how fast that gets done. So integrating logging with monitoring can help sift through this data much more quickly to solve customer experience issues caused by a slow-working application.

It gives us clear understanding of the behaviour of our applications and in debugging in simple terms

Now a days Important information of a business can be obtained from logs.

Like,  User preferences 
	System important datas
	Security threats
	Competitive analysis etc

Testing team should consider monitory the logs on a regular basis is important.

Most logging frameworks have a set of logging levels similar to the following: fatal, error, warning, info or debug. 
If you’re only logging errors, which is often the default and only certain types of info, you may not run into any issues.

But as soon as you increase your logging level to debugging, which you may be using when in development, you could start having some disk space concerns. This may not be an issue if it’s one application. 
But if multiple applications are running, system resources could be affected.

So we must take care of WHAT WE LOG AND WHERE WE LOG.

Unfortunately the JDK did not include logging in its original release so by the time the Java Logging API was added several other logging frameworks had become widely used - in particular Apache Commons Logging (also known as Java Commons Logging or JCL) and log4J. This led to problems when integrating different third-party libraries (JARs) each using different logging frameworks. Pluggable logging frameworks (wrappers) were developed to solve this problem.


Building Blocks of logging : 
		
			The Logger 
			The Formatter
            The Filter
			The Appender (or Handler)

The Logger is responsible for capturing the message to be logged along with certain metadata and passing it to the logging framework.

After receiving the message, the framework calls the Formatter with the message which formats it for output.
        eg: SimpleFormatter
            XMLFormatter

The Filter can filter out log messages, meaning decide if the message gets logged or not.

The framework then hands the formatted message to the appropriate Appender/Handler for disposition. This might include output to a console display, writing to disk, appending to a database, or generating an email. 
        eg: ConsoleHandler
            FileHandler
            StreamHandler
            SocketHandler
            MemoryHandler


Logging Levels:

The standard ranking of logging levels is as follows: ALL < TRACE < DEBUG < INFO < WARN < ERROR < FATAL < OFF.

OFF

This log level does not log anything. This OFF level is used to turn off logging and is the greatest possible rank. With this log level, nothing gets logged at all.

FATAL

FATAL means that the application is about to stop a serious problem or corruption from happening. The FATAL level of logging shows that the application’s situation is catastrophic, such that an important function is not working. For example, you can use FATAL log level if the application is unable to connect to the data store.

ERROR

Unlike the FATAL logging level, error does not mean your application is aborting. Instead, there is just an inability to access a service or a file. This ERROR shows a failure of something important in your application. This log level is used when a severe issue is stopping functions within the application from operating efficiently. Most of the time, the application will continue to run, but eventually, it will need to be addressed.

WARN

The WARN log level is used when you have detected an unexpected application problem. This means you are not quite sure whether the problem will recur or remain. You may not notice any harm to your application at this point. This issue is usually a situation that stops specific processes from running. Yet it does not mean that the application has been harmed. In fact, the code should continue to work as usual. You should eventually check these warnings just in case the problem reoccurs.

INFO

INFO messages are like the normal behavior of applications. They state what happened. For example, if a particular service stopped or started or you added something to the database. These entries are nothing to worry about during usual operations. The information logged using the INFO log is usually informative, and it does not necessarily require you to follow up on it.

DEBUG

With DEBUG, you are giving diagnostic information in a detailed manner. It is verbose and has more information than you would need when using the application. DEBUG logging level is used to fetch information needed to diagnose, troubleshoot, or test an application. This ensures a smooth running application.

TRACE

The TRACE log level captures all the details about the behavior of the application. It is mostly diagnostic and is more granular and finer than DEBUG log level. This log level is used in situations where you need to see what happened in your application or what happened in the third-party libraries used. You can use the TRACE log level to query parameters in the code or interpret the algorithm’s steps.

ALL

This log level logs any logging levels that are defined. It logs everything and includes custom logging levels as well. It is the combination of all other logging levels.


Logging best practices:

1. Use a Standard Logging Library

Things to consider and evaluate are performance, flexibility, appenders for new log centralization solutions, and so on. If you tie yourself directly to a single framework the switch to a newer library can take a substantial amount of work and time. Keep that in mind and go for the API that will give you the flexibility to swap logging libraries in the future. Just like with the switch from Log4j to Logback and to Log4j 2, when using the SLF4J API the only thing you need to do is change the dependency, not the code.

2. Select Your Appenders Wisely

Appenders define where your log events will be delivered. The most common appenders are the Console and File Appenders.

3. Use Meaningful Messages

Your log events should include messages that are unique to the given situation, clearly describe them and inform the person reading them. Imagine a communication error occurred in your application. You might do it like this:

LOGGER.warn("Communication error");
But you could also create a message like this:

LOGGER.warn("Error while sending documents to your server, response code %d, response message %s. The message sending will be retried.", responseCode, responseMessage)

4. Logging Java Stack Traces

    public static void main(String[] args) {
        try {
            throw new IOException("This is an I/O error");
        } catch (IOException ioe) {
            LOGGER.error("Error while executing main thread", ioe);
        }
    }

11:30:17.527 ERROR - Error while executing main thread
java.io.IOException: This is an I/O error
    at com.logging.main(Log4JException.java:13) [main/:?]

It contains relevant information – i.e. the name of the class, the method where the problem occurred, and finally the line number where the problem happened. Of course, in real-life situations, the stack traces will be longer, but you should include them to give you enough information for proper debugging.

5. Keep the Log Structure Consistent

The structure of your log events should be consistent. This is not only true within a single application or set of microservices, but should be applied across your whole application stack. With similarly structured log events it will be easier to look into them, compare them, correlate them, or simply store them in a dedicated data store.

6. Add Context to Your Logs

Information context is important and for us developers and DevOps a log message is information. Look at the following log entry:

[2020-06-29 16:25:34] [ERROR ] An error occurred!

We know that an error appeared somewhere in the application. We don’t know where it happened, we don’t know what kind of error it was, we only know when it happened. Now look at a message with slightly more contextual information:

[2020-06-29 16:25:34] [main] [ERROR ] com.logging.ParsingErrorExample - A parsing error occurred for user with id 1234!

The same log record, but a lot more contextual information. We know the thread in which it happened, we know what class the error was generated at. We modified the message as well to include the user that the error happened for, so we can get back to the user if needed. We could also include additional information like diagnostic contexts. Think about what you need and include it.

We have something like the PatternLayout in Log4J2 that gives you all that you need to include context information.

7. Don’t Log Too Much or Too Little

8. Avoid Logging Sensitive Information

9. better to usea  Log Management Solution

How do we make the logs much more useful? Through structuring those logs.

What Can Structured Logging Do For Us?

Customers often feel that support for business analytics is a much lower priority than adding new features. After all, we can always add that stuff later, right? My experience is that by the time "later" comes, the effort to modify the software has become prohibitive… unless you’ve been using structured logging all along. In that case, adding business analytics support turns out to be very easy to do. In many cases, all you need to do is to create some canned reports using the log analysis tools.

Here are a few other questions that structured logging can help us answer easily if it is implemented from the very beginning:

Diagnostics

What caused this stack trace?

What was the sequence of events that led up to this request failing unexpectedly?

Analytics

Who is using our service?

What does usage look like over time?

What are our customers using our system to do?

Monitoring

How long is it taking to process a request?

How much available memory is there?

The idea of structured logging is to take an application log that is delivered as a string of text and convert it into a simple relational data set that can be more easily searched and analyzed.

Say your application lets users create reports, which you want to log. The bare minimum log message for that could look like this:

2021-07-29 | New report created

You have the date in ISO-8601 format, followed by the message. It could use some more context, such as the time of day and a log level to express the severity of the event:

2021-07-29 14:52:55.1623|INFO|New report created

Things are getting better. Let’s also include the ID of the user who created the report:

2021-07-29 14:54:55.1623|INFO|New report created by user 4253

It wouldn’t be a stretch to imagine log events recording different occurrences:

INFO|New report created by user 4253
INFO|Report updated by user 257
INFO|User 478 deleted report 

As you can see, users can also change and delete reports. Also, the last example doesn’t use the same format as the other two.

Now comes the tricky part. Let’s say you need to search through your log events to find all instances of a given user performing some action to reports. That’s not so easy to do, thanks to the inconsistent format of the messages.

Besides reports, users can create other types of artifacts, and such activities are also logged. With the right amount of regex, you’ll probably be able to pull it off. However, such code is error-prone, fragile, and doesn’t generate the most value for you and your customers.

Structured Logging to the Rescue:

Structured logging solves the above problems by generating easily parsable logs. For instance, the following is an example of how we could structure the events in the example using JSON:

{
    "TimeStamp": "2021-07-29 14:52:55.1623",
    "Level": "Info",
    "Message": "New report created",
    "UserId": "4253",
    "ReportId": "4567",
    "Action": "Report_Creation"
}

We have properties that indicate what action occurred and the identifications of the relevant objects, such as the user and the report created. Parsing a collection of events in the format above makes it easier to search through events than it would be with plain text.

Logging frameworks:


Apache Log4j

Apache Log4j is a very old logging framework and was the most popular one for several years. It introduced basic concepts, like hierarchical log levels and loggers, that are still used by modern logging frameworks.
you can use the SLF4JAPI that I showed you earlier to write log messages with Log4j

Logback

It follows the same concepts as Log4j but was rewritten to improve the performance, to support SLF4J natively, and to implement several other improvements like advanced filtering options and automatic reloading of logging configurations.

Apache Log4j2

 it also allows lazy evaluation of log statements based on lambda expressions, offers asynchronous loggers for low-latency systems, and provides a garbage-free mode to avoid any latency caused by garbage collector operations.


Writing Log Messages with SLF4J

Writing log messages with SLF4J is very easy. You first need to call the getLogger method on the LoggerFactory to instantiate a new Logger object. we can call any logger methods then and print out the msg.

In Short What JPA is for RDBMS, SLF4J is for Log Providers