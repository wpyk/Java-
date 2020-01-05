 - StringBuilder
 - io.thread.exception

# 1.jeytty的使用  

在工程根目录下按住shift和鼠标右键，选择在此处打开powershell
运行mvn clean compile
运行mvn jetty:run
在chrome里输入url：127.0.0.1:8080/path


public class SearchController{

    @GetMapping("/search")
    public String Search(@requestParam(name="keyword", required= true) String keyword, Model model){

        if("weather".equals(keyword)){
            model.addAttribute("error", windy);
        }else{
            model.addAttribute("error", not find);
        }
        return "search";

    }
    
}