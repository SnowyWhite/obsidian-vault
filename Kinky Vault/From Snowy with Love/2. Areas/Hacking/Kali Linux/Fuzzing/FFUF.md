**Find directories and webfiles simultaneously**

```bash
ffuf -u http://localhost:8000/FUZZ -w /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt -fc 403 -sf -ic -od /home/kali/Documents/webdiplomacy/ffuf -maxtime 10 -timeout 7 -e .asp,.aspx,.bat,.c,.cfm,.cgi,.css,.com,.dll,.exe,.htm,.html,.inc,.jhtml,.js,.jsa,.jsp,.log,.mdb,.nsf,.pcap,.php,.php2,.php3,.php4,.php5,.php6,.php7,.phps,.pht,.phtml,.pl,.reg,.sh,.shtml,.sql,.swf,.txt,.xml
```