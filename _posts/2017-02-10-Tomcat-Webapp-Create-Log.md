---
layout: post
title: 手动实现log4j的写入日志文件log.txt
date: 2017-02-10
categories: blog
tags: [Java]
description: 模拟实现log4j的写入日志文件功能。

---

如何把servlet运行结果保存到log.txt中。


```
import javax.servlet.http.*;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;

public class CheckSequenceLog extends HttpServlet{	
    File log;//Refer to log.txt
    FileOutputStream logging; //Use to write to log.txt

    int sequence=0;//Indicate the running order
    String text;//The text to write in the log.txt

    public void init(){
        try{
            log = new File("../webapps/SelfIntro_Qin_Peng/log.txt");//Create a log.txt in the root directory of the web app.
            //log = new File("C:\\Programs\\apache-tomcat-7.0.69\\webapps\\SelfIntro_Qin_Peng\\log.txt");//Work
            //log = new File("../log.txt");//Create new file in directory:/apache-tomcat-7.0.69/
            logging = new FileOutputStream(log,true);//Not forget new

            sequence++;
            text = "inti():"+sequence+"\n";

            System.out.println(text);//Log in the command line

            logging.write(text.getBytes());//Write the log in the log.txt
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(Exception e){
            e.printStackTrace();
        }
    }

    public void service(HttpServletRequest req, HttpServletResponse resp)throws java.io.IOException{
        try{
            sequence++;
            text = "service():"+sequence+"\n";

            resp.getWriter().println(text);//Write the log in the website
            logging.write(text.getBytes());
        }catch(Exception e){
            e.printStackTrace();
        }	
    }

    public void destroy(){
        try{
            sequence++;
            text = "destroy():"+sequence+"\n";

            System.out.println(text);
            logging.write(text.getBytes());

            logging.close();
            //log.close();//File没有close()
        }catch(Exception e){
            e.printStackTrace();
        }
    }

}
```

---










