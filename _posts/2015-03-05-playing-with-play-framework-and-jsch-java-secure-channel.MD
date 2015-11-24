---
layout: post
title: Playing with Play Framework and JSch - Java Secure Channel
date: 2015-03-05 14:06:29.000000000 -03:00
type: post
published: true
status: publish
categories:
- java
- jsch
- play framework
comments: true
---
Today I'm gonna show you how to use the the Java library _JSch - Java Secure Channel_ to connect to a server and send SSH commands to a UNIX shell and then return the output to our webpage. I'm using _Play Framework_ to develop this webapp. If you want to know more about Play Framework just visit [http://www.playframework.com](http://www.playframework.com "http://www.playframework.com")  
<br />
A little bit about _JSch_:
_JSch_ is a pure Java implementation of <a href="http://ietf.org/html.charters/secsh-charter.html" target="_blank">SSH2</a>.  
_JSch_ allows you to connect to an sshd server and use port forwarding, X11 forwarding, file transfer, etc., and you can integrate its functionality into your own Java programs. _JSch_ is licensed under <a href="http://www.jcraft.com/jsch/LICENSE.txt">BSD style license</a>.</p>
You can find more information about the library in <a href="http://www.jcraft.com/jsch/">http://www.jcraft.com/jsch/</a>
<br /><br />**Case scenario:**  
I want to send a SSH command to an UNIX server via some Java class. I want to the output of this command that I sent is shown in the user's screen through the web browser.
Our environment uses a Private Key to allow SSH connections between one machine to another. In the code snippets you will see that the keys are passed through the method:    
<br />
```
jsch.addIdentity();
```
<br />
<br />
1st: the code snippet for the controller _Application.java_:  


```java
package controllers;

import oi.siebel.Control; //that's the Class I created to send the SSH commands to an UNIX shell
import play.mvc.Controller;
import play.mvc.Result;
import java.util.*;
import java.lang.*;

public class Application extends Controller {

        public static Result index() {

            //variable that will receive the result of the method listOHSParam
            String result = null;

            try {
                oi.siebel.Control a = new Control();
                HashMap<String, String[]> result = null;
                HashMap<String, Integer> result2 = null;
                String[] result3 = null;
                HashMap<String, String> result4 = null;
                Iterator it = null;

                resultado = a.listOHSParam(Control.EnvironmentOptions.NonProduction, "server01", "/siebel/MiddlewareHome/Oracle_WT1/instances/instance1");

            }
            catch (Exception ex){

            }
            finally {

            }

            return ok(result);
        }

}
```
<br />
2nd: the code snippet for the controller Control.java:   

```java
package controllers;

import com.jcraft.jsch.ChannelExec;
import com.jcraft.jsch.JSch;
import com.jcraft.jsch.Session;

import java.io.ByteArrayOutputStream;
import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;

public class Control {

    public enum EnvironmentOptions { Production, NonProduction };
    private String user = "admin";
    private String sshKeyPRD = "/home/workspace/testeJava/admin_open.ppk";
    private String sshPassPRD = "#########"; //password hidden for security reasons
    private String sshKeyHML = "/home/workspace/testeJava/admin_tst_priv_openssh.ppk";


    //constructor
    public Control() { }

    private com.jcraft.jsch.JSch createJSchObjetc(EnvironmentOptions env) throws Exception {
        try {
            com.jcraft.jsch.JSch jsch = new JSch();
            if (env == EnvironmentOptions.Production) {
                jsch.addIdentity(sshKeyPRD,sshPassPRD);
            }
            else {
                jsch.addIdentity(sshKeyHML);
            }
            return jsch;
        }
        catch (Exception e) {
            throw new Exception(e);
        }
    }

    //=========================================================================================
    // Metodo...: listOHSParam
    // Descricao: List all parameters of the HTTPD.CONF file from OHS - Oracle HTTP Server
    //=========================================================================================
    public String listOHSParam(EnvironmentOptions env, String server, String ohsInstanceHome) throws Exception {

        ChannelExec channel=null;
        Session session=null;
        String result="";

        try{
            // Create object to send the SSH command
            JSch jsch = createJSchObjetc(env);

            // Create object Session and do the SSH conection
            session=jsch.getSession(user, server, 22);
            session.setConfig("StrictHostKeyChecking", "no");
            session.connect();

            // Defines the command
            String command = "cat " + ohsInstanceHome + "/config/OHS/ohs1/httpd.conf";

            // Create object Channel
            channel=(ChannelExec)session.openChannel("exec");
            channel.setCommand(command);
            ByteArrayOutputStream error=new ByteArrayOutputStream();
            channel.setErrStream(error);
            channel.connect();

            DataInputStream dataIn = new DataInputStream(channel.getInputStream());
            DataOutputStream dataOut = new DataOutputStream(channel.getOutputStream());

            // Get the response and add to the HashMap
            String line;
            while ((line = dataIn.readLine()) != null) {
                result += line + "\n";
            }

            dataIn.close();
            dataOut.close();
        }
        catch (Exception e) {
            throw new Exception(e);
        }
        finally {
            if (channel != null){
                channel.disconnect();
                session.disconnect();
            }
        }

        return result;
    }

}
```  
<br />
Output of the command being displayed in a web browser:  
<br />![Genealogical_Tree]({{ site.url }}/assets/images/play-JSch.png)  
<br />That's all folks. See ya next time!
