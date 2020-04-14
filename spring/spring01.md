#spring01传统的工厂模式解耦
传统模式contorller,service,dao层层相连，耦合度过高，无法更换其中的某层
使用工厂加配置文件的方式能实现解耦

```
package com.factory;

import java.io.InputStream;
import java.util.Enumeration;
import java.util.HashMap;
import java.util.Map;
import java.util.Properties;

/**
 * 先初始化所有类，需要时全部取出使用
 */
public class BeanFactory {
    private static Properties properties;
    private static Map<String, Object> beans;

    static {
        try {
            properties = new Properties();
            InputStream in = BeanFactory.class.getClassLoader().getResourceAsStream("bean.properties");
            properties.load(in);
            beans = new HashMap<String, Object>();
            Enumeration keys = properties.keys();
            while (keys.hasMoreElements()) {
                String key = keys.nextElement().toString();
                String beanPath = properties.getProperty(key);
                Object value = Class.forName(beanPath).newInstance();
                beans.put(key, value);
            }
        } catch (Exception e) {
            throw new ExceptionInInitializerError("初始化配置文件失败");
        }
    }
    public static Object getBean(String beanName) {
        return beans.get(beanName);
    }

}
```


这样contorller层获取service对象时可以通过BeanFactory读取配置文件获取
service层获取Dao层是也可以这样
降低了各组件的耦合性
