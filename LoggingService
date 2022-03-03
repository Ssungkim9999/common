package common;

import org.slf4j.*;

public class LoggingService {

	private static Logger createLogger(Class className) {
		return LoggerFactory.getLogger(className);
	}
	
	public static void info(Class className, String logData) {
		createLogger(className).info(logData);
	}
	
	public static void debug(Class className, String logData) {
		createLogger(className).debug(logData);
	}
	
	public static void error(Class className, String logData, Exception e) {
		createLogger(className).error(logData);
		e.printStackTrace();
	}
	
	public static boolean isInfoEnabled(Class className) {
		return createLogger(className).isInfoEnabled();
	}
	
	public static void sessionExpired(Class className) {
		createLogger(className).info("Session is expired.");
	}
}
