package common;

import java.util.*;
import org.springframework.web.servlet.*;

public class CommonController {
  /**
   * @author Ssungkim9999
   * @param page
   * @param param
   * @param className
   * @return ModelAndView contains all parameters and page info. Using for normal page move.
  */
  public static ModelAndView returnPage(String page, DataMap param, Class className) {
    ModelAndView mav = new ModelAndView();
    mav.setViewName("/WEB-INF/view/comm/layout.jsp");
    mav.addObject("page", "/WEB-INF/view/"+page+".jsp");
    LoggingService.info(className, "direction page ::: "+page);
    if(param != null) {
      Set<String> set = param.keySet();
      Iterator<String> it = set.iterator();
      while(it.hasNext()) {
        String key = it.next();
        Object value = param.get(key);
        mav.addObject(key, value);
      }
    }
    return mav;
  }

  /**
   * @author Ssungkim9999
   * @param page
   * @param param
   * @param className
   * @return ModelAndView contains all parameters and page info. Using for Ajax return page.
  */
  public static ModelAndView returnView(String page, DataMap param, Class className) {
    ModelAndView mav = new ModelAndView();
    mav.setViewName("/WEB-INF/view/"+page+".jsp");
    LoggingService.info(className, "direction page ::: "+page);
    if(param != null) {
      Set<String> set = param.keySet();
      Iterator<String> it = set.iterator();
      while(it.hasNext()) {
        String key = it.next();
        Object value = param.get(key);
        mav.addObject(key, value);
      }
    }
    return mav;
  }
}
