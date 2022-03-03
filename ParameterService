package common;

import java.io.*;
import java.util.*;
import java.util.regex.*;
import javax.servlet.http.*;
import org.springframework.web.multipart.*;

public class ParameterService {
	/**
	 * @author Ssungkim9999
	 * @param req
	 * @param key
	 * @return If parameter value is null then return blank String value, Otherwise return String value that is data about key on request.
	*/
	public static String getStringParameter(HttpServletRequest req, String key) {
	  return req.getParameter(key) == null ? "" : replaceDataRegex(3, req.getParameter(key).toString());
	}

	/**
	 * @author Ssungkim9999
	 * @param req
	 * @param key
	 * @return Integer value on key from request parameter.
	*/
	public static int getIntegerParameter(HttpServletRequest req, String key) {
	  int n = 0;
	  try {
	    n = req.getParameter(key) == null ? 0 : Integer.parseInt(req.getParameter(key).toString());
	  } catch(Exception e) {
	    LoggingService.error("ParameterService".getClass(), "Exception for parsing int data from request. key : "+key+" / data : "+req.getParameter(key), e);
	  }
	  return n;
	}

	/**
	 * @author Ssungkim9999
	 * @param req
	 * @param key
	 * @return Boolean value on key from request paramter.
	*/
	public static boolean getBooleanParameter(HttpServletRequest req, String key) {
	  boolean b = false;
	  try {
	    b = req.getParameter(key) == null ? false : Boolean.parseBoolean(req.getParameter(key));
	  } catch(Exception e) {
	    LoggingService.error("ParameterService".getClass(), "Exception for parsing boolean data from request. key : "+key+" / data : "+req.getParameter(key), e);
	  }
	  return b;
	}

	/**
	 * @author Ssungkim9999
	 * @param req
	 * @param key
	 * @return String array on key from request parameter.
	*/
	public static String[] getStringArrayParameter(HttpServletRequest req, String key) {
	  String[] ar = req.getParameterValues(key);
	  if(ar == null) {
	    ar = req.getParameterValues(key+"[]");
	    if(ar == null) return new String[0];
	  }
	  else {
	    int len = ar.length;
	    for(int i=0; i<len; i++) {
	      String s = ar[i];
	      s = replaceDataRegex(3, s);
	      ar[i] = s;
	    }
	  }
	  return ar;
	}

	/**
	 * @author Ssungkim9999
	 * @param req
	 * @return DataMap contains all parameter data.
	*/
	public static DataMap makeAllParameterToMap(HttpServletRequest req) {
	  DataMap param = new DataMap();
	  Enumeration<String> keys = req.getParameterNames();
	  while(keys.hasMoreElements()) {
	    String key = keys.nextElement();
	    Object value = req.getParameter(key);
	    param.put(key, value);
	  }
	  return param;
	}

	/**
	 * @author Ssungkim9999
	 * @param mreq
	 * @param key
	 * @param dir
	 * @param name
	 * @return File is that had directory is Dir on parameter and name is Name on parameter.
	*/
	public static File getFileParameter(MultipartHttpServletRequest mreq, String key, String dir, String name) {
	  MultipartFile file = mreq.getFile(key);
	  File f = null;
	  if(file != null) {
	    f = new File(dir, name);
	    try {
	      file.transferTo(f);
	      LoggingService.info("ParameterService".getClass(), "Success to make file about "+key+". Dir : "+dir+" / Name : "+name);
	    } catch(Exception e) {
	      LoggingService.error("ParameterService".getClass(), "Exception for transfer file. dir : "+dir+" / name : "+name, e);
	    }
	  }
	  return f;
	}

	/**
	 * @author Ssungkim9999
	 * @param type
	 * @return String value regex data on type.
	*/
	private static String regex(int type) {
	  String regex = "";
	  switch(type) {
	  case 0:			// 아이디
	    regex = "[^a-zA-Z0-9_]";
	    break;
	  case 1: 		// 비밀번호
	    regex = "[^a-zA-Z0-9!@#$%^&*?_~]";		// !@#$%^&*?_~
	    break;
		case 2: 		// 이메일
			regex = "^([\\w-]+(?:\\.[\\w-]+)*)@((?:[\\w-]+\\.)*\\w[\\w-]{0,66})\\.([a-z]{2,6}(?:\\.[a-z]{2})?)$";
			break;
	  case 3:			// 특수문자 치환
	    regex = "(&gt;)|(&lt;)|(&amp;)|(&quot;)|(&#39;)";		// > < & " '
	    break;
	  case 4:			// 숫자
	    regex = "[^0-9]";
	    break;
	  case 5:			// 수신번호 1
	    regex = "^(01[16789])([2-9]{1}[0-9]{2})([0-9]{4})$";
	    break;
	  case 6:			// 수신번호 2
	    regex = "^(01[016789])([2-9]{1}[0-9]{3})([0-9]{4})$";
	    break;
	  }
	  return regex;
	}

	/**
	 * @author Ssungkim9999
	 * @param type
	 * @param data
	 * @return String data that is changed to regex data.
	 * @explain type 0 - id / 1 - password / 2 - email (not used) / 3 - special characters / 4 - number / 5 - number for Callnum(3-3-4) / 6 - number for Callnum(3-4-4)
	*/
	public static String replaceDataRegex(int type, String data) {
	  Pattern pattern = Pattern.compile(regex(type));
	  Matcher matcher = pattern.matcher(data);
	  while(matcher.find()) {
	    if(type == 3) data = data.replace("&gt;", ">").replace("&lt;", "<").replace("&amp;", "&").replace("&quot;", "\"").replace("&#39;", "'");
	    else data = data.replace(matcher.group(), "");
	  }
	  return data;
	}
}
