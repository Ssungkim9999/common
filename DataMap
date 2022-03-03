package common;

import java.io.*;
import java.util.*;

@SuppressWarnings("serial")
public class DataMap extends HashMap<String, Object>{

	@Override
	public Object put(String key, Object value) {
		// TODO Auto-generated method stub
		return super.put(key, value);
	}
	
	@Override
	public Object get(Object key) {
		// TODO Auto-generated method stub
		return super.get(key);
	}
	
	@Override
	public String toString() {
		// TODO Auto-generated method stub
		return super.toString();
	}
	
	/**
	 * @author Ssungkim9999
	 * @param key
	 * @return String value that is got from Map. If value is null, return blank String value. Otherwise return value.toString().trim().
	 */
	public String getString(Object key) {
		return super.get(key) == null ? "" : super.get(key).toString().trim();
	}
	
	/**
	 * @author Ssungkim
	 * @param key
	 * @return Integer value that is got from Map. If value is null, return 0. Otherwise return Integer.parseInt(value.toString().trim()).
	 */
	public int getInt(Object key) {
		Object o = super.get(key);
		int n = 0;
		try {
			String s = o == null ? "0" : o.toString().trim();
			s = CommonService.replaceDataRegex(4, s);
			n = Integer.parseInt(s);
		} catch(Exception e) {
			LoggingService.error(getClass(), "Exception for parsing data... key : "+key+" / data : "+o, e);
		}
		return n;
	}
	
	/**
	 * @author Ssungkim9999
	 * @param key
	 * @return Boolean value that is got from Map. If value is null, return false. Otherwise return value that is parsed data.
	 */
	public boolean getBoolean(Object key) {
		try {
			return super.get(key) == null ? false : Boolean.parseBoolean(super.get(key).toString().trim());
		} catch(Exception e) {
			LoggingService.error(getClass(), "Exception for parsing data... key : "+key+" / data : "+super.get(key), e);
			return false;
		}
	}
	
	/**
	 * @author Ssungkim9999
	 * @param key
	 * @return File data that is got from Map. If file is null, return null.
	 */
	public File getFile(Object key) {
		try {
			return super.get(key) == null ? null : (File)super.get(key);
		} catch(Exception e) {
			LoggingService.error(getClass(), "Exception for convert data to File... key : "+key, e);
			return null;
		}
	}
}
