@Scheduled 标记要调度的方法的注解  


源码阅读：
```java
package org.springframework.scheduling.annotation;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Repeatable;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

/**
 * An annotation that marks a method to be scheduled.(这个注解用来标识定时任务) Exactly one of
 * the {@link #cron()}, {@link #fixedDelay()}, or {@link #fixedRate()}
 * attributes must be specified.(cron fixedDelay fixedRate三选一，至少要有一个)
 *
 * <p>The annotated method must expect no arguments. It will typically have
 * a {@code void} return type; if not, the returned value will be ignored
 * when called through the scheduler.（不能有入参，返回值通常为void，有返回值也会在调用定时任务的时候被忽略）
 *
 * <p>Processing of {@code @Scheduled} annotations is performed by
 * registering a {@link ScheduledAnnotationBeanPostProcessor}. This can be
 * done manually or, more conveniently, through the {@code <task:annotation-driven/>}
 * element or @{@link EnableScheduling} annotation.（利用注解@Scheduled注解的过程，会被ScheduledAnnotationBeanPostProcessor注册，可以手动执行，也可以使用xml或者注解开启相关设置，自动完成）
 *
 * <p>This annotation may be used as a <em>meta-annotation</em> to create custom
 * <em>composed annotations</em> with attribute overrides.（这个注解可以视为元注解，在此基础上实现自定义注解）
 *
 * @author Mark Fisher
 * @author Juergen Hoeller
 * @author Dave Syer
 * @author Chris Beams
 * @since 3.0
 * @see EnableScheduling
 * @see ScheduledAnnotationBeanPostProcessor
 * @see Schedules
 */
@Target({ElementType.METHOD, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Repeatable(Schedules.class)
public @interface Scheduled {

	/**
	 * A cron-like expression, extending the usual UN*X definition to include triggers
	 * on the second as well as minute, hour, day of month, month and day of week.
	 * <p>E.g. {@code "0 * * * * MON-FRI"} means once per minute on weekdays
	 * (at the top of the minute - the 0th second).
	 * @return an expression that can be parsed to a cron schedule
	 * @see org.springframework.scheduling.support.CronSequenceGenerator
	 */
	String cron() default "";
    //（定时任务触发时机，参数有6个从左到右以此表示[秒] [分] [小时] [日] [月] [周]），CronSequenceGenerator中有具体说明
    //0 * * * * MON-FRI 表示每个工作日，每一分钟执行一次
    //0 0/10 * * * ? 表示每天，每十分钟执行一次

	/**
	 * A time zone for which the cron expression will be resolved. By default, this
	 * attribute is the empty String (i.e. the server's local time zone will be used).
	 * @return a zone id accepted by {@link java.util.TimeZone#getTimeZone(String)},
	 * or an empty String to indicate the server's default time zone
	 * @since 4.0
	 * @see org.springframework.scheduling.support.CronTrigger#CronTrigger(String, java.util.TimeZone)
	 * @see java.util.TimeZone
	 */
	String zone() default "";
    //时区，默认为空，使用服务器使用的时区

	/**
	 * Execute the annotated method with a fixed period in milliseconds between the
	 * end of the last invocation and the start of the next.
	 * @return the delay in milliseconds
	 */
	long fixedDelay() default -1;
    //上一次调用结束后指定时间开始执行下一次

	/**
	 * Execute the annotated method with a fixed period in milliseconds between the
	 * end of the last invocation and the start of the next.
	 * @return the delay in milliseconds as a String value, e.g. a placeholder
	 * or a {@link java.time.Duration#parse java.time.Duration} compliant value
	 * @since 3.2.2
	 */
	String fixedDelayString() default "";
    //与fixedDelay相同效果，只是使用字符串的形式

	/**
	 * Execute the annotated method with a fixed period in milliseconds between
	 * invocations.
	 * @return the period in milliseconds
	 */
	long fixedRate() default -1;
    //两次调用时间间隔

	/**
	 * Execute the annotated method with a fixed period in milliseconds between
	 * invocations.
	 * @return the period in milliseconds as a String value, e.g. a placeholder
	 * or a {@link java.time.Duration#parse java.time.Duration} compliant value
	 * @since 3.2.2
	 */
	String fixedRateString() default "";
    //与fixedRate相同效果，只是使用字符串的形式

	/**
	 * Number of milliseconds to delay before the first execution of a
	 * {@link #fixedRate()} or {@link #fixedDelay()} task.
	 * @return the initial delay in milliseconds
	 * @since 3.2
	 */
	long initialDelay() default -1;
    //第一次执行fixedRate或者fixedDelay之前的时间间隔

	/**
	 * Number of milliseconds to delay before the first execution of a
	 * {@link #fixedRate()} or {@link #fixedDelay()} task.
	 * @return the initial delay in milliseconds as a String value, e.g. a placeholder
	 * or a {@link java.time.Duration#parse java.time.Duration} compliant value
	 * @since 3.2.2
	 */
	String initialDelayString() default "";
    //与initialDelay相同效果，只是使用字符串的形式
}


```


时间格式说明：  
参考：  
1. https://www.cnblogs.com/ark-blog/p/9000079.html  
2. https://cron.qqe2.com/（在线生成cron表达式）




























