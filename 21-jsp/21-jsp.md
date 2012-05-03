# Java Server Pages #

Szerveroldali Java (ez az, ahol a Java er�s).

Kis t�rt�neti �ttekint�s:
* gohper://
* Statikus HTML
* Dinamikus HTML, CGI (elkezdt�k arra haszn�lni, amire nem val�)
* Szerver oldali scriptel�s (PHP/MySQL)

	```php
	<html>
	 <head>
	  <title>PHP Test</title>
	 </head>
	 <body>
	 <? echo '<p>Hello World</p>'; ?> 
	 </body>
	</html>
	```

* �j: mindenhol JS...

## El�zm�ny: Szervletek ##

* [JSR 315](http://www.jcp.org/en/jsr/detail?id=315) - Servlet 3.0 (aktu�lis, 2009 �ta)
* [JSR 154](http://www.jcp.org/en/jsr/detail?id=154) - Servlet 2.4/2.5
* [JSR 53](http://www.jcp.org/en/jsr/detail?id=53) - Servlet 2.3

Java szervlet implement�ci� --> M�gi�k --> M�g t�bb m�gi�k --> Dinamikusan el��ll�tott weboldal

``` java
package hello;
 
import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
 
public class HelloServlet extends HttpServlet {
 
    @Override
    public void init(ServletConfig config) throws ServletException {
        super.init(config);
        getServletContext().log("init()");
    }
 
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        getServletContext().log("service()");
        response.getWriter().write("Hello World!");
    }
 
    @Override
    public void destroy() {
        getServletContext().log("destroy()");
    }
}

```

## Ugyanez JSP form�tumban ###

``` jsp
<%@page contentType="text/html" pageEncoding="UTF-8"%>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
   "http://www.w3.org/TR/html4/loose.dtd">

<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>JSP Page</title>
    </head>
    <body>
        <%
            getServletContext().log("service()");
            response.getWriter().write("Hello World!");
        %>
    </body>
</html>
```

Ebb�l gener�l�dok egy ehhez hasonl� szervlet:

``` java
package org.apache.jsp;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.jsp.*;

public final class FirstJsp extends org.apache.jasper.runtime.HttpJspBase
    implements org.apache.jasper.runtime.JspSourceDependent {

  private static final JspFactory _jspxFactory = JspFactory.getDefaultFactory();

  private static java.util.Vector _jspx_dependants;

  private org.apache.jasper.runtime.ResourceInjector _jspx_resourceInjector;

  public Object getDependants() {
    return _jspx_dependants;
  }

  public void _jspService(HttpServletRequest request, HttpServletResponse response)
        throws java.io.IOException, ServletException {

    PageContext pageContext = null;
    HttpSession session = null;
    ServletContext application = null;
    ServletConfig config = null;
    JspWriter out = null;
    Object page = this;
    JspWriter _jspx_out = null;
    PageContext _jspx_page_context = null;

    try {
      response.setContentType("text/html;charset=UTF-8");
      pageContext = _jspxFactory.getPageContext(this, request, response,
      			null, true, 8192, true);
      _jspx_page_context = pageContext;
      application = pageContext.getServletContext();
      config = pageContext.getServletConfig();
      session = pageContext.getSession();
      out = pageContext.getOut();
      _jspx_out = out;
      _jspx_resourceInjector = (org.apache.jasper.runtime.ResourceInjector) application.getAttribute("com.sun.appserv.jsp.resource.injector");

      out.write("\n");
      out.write("\n");
      out.write("\n");
      out.write("<!DOCTYPE HTML PUBLIC \"-//W3C//DTD HTML 4.01 Transitional//EN\"\n");
      out.write("   \"http://www.w3.org/TR/html4/loose.dtd\">\n");
      out.write("\n");
      out.write("<html>\n");
      out.write("    <head>\n");
      out.write("        <meta http-equiv=\"Content-Type\" content=\"text/html; charset=UTF-8\">\n");
      out.write("        <title>JSP Page</title>\n");
      out.write("    </head>\n");
      out.write("    <body>\n");
      out.write("        ");

            getServletContext().log("service()");
            response.getWriter().write("Hello World!");
        
      out.write("\n");
      out.write("    </body>\n");
      out.write("</html>\n");
    } catch (Throwable t) {
      if (!(t instanceof SkipPageException)){
        out = _jspx_out;
        if (out != null && out.getBufferSize() != 0)
          out.clearBuffer();
        if (_jspx_page_context != null) _jspx_page_context.handlePageException(t);
      }
    } finally {
      _jspxFactory.releasePageContext(_jspx_page_context);
    }
  }
}
```

### Egy�b form�tumok ####

* Expression:
	
	``` java
	<%= new java.util.Date() %>
	```	

* Scriplet
	
	``` java
	<%
		out.println(new java.util.Date());
	%>
	```

* Deklar�ci�k:

	``` java
	<%!
	    final Date creationDate = new Date();
	    public Date getDate() {
		return creationDate;
	    }
	%>
	```

* Import utas�t�sok:

	``` java
	<%@ page import="java.util.*" %>
	<html>
	...
	</html>
	```

* Tag-ek:

	``` java
	<jsp:include page="header.jsp"/>
	```

* HTML �s JSP utas�t�sok vegy�t�se:

	```java
	<%
	    String name = (String)request.getParameter("name");
	    if ( name != null ) {
	%>
		Hi <%= name %>!
	<%
	    } else {
	%>
		Hi Anonymous!
	<%
	    }
	%>
	```

### El�rhet� objektumok ###

* `HttpServletResponse response`: content type be�ll�t�sa, `Writer`, cookie-k be�ll�t�sa, session, ezen kereszt�l �rhet� el, etc.
* `HttpServletRequest request`: param�terek, session, cookie-k lek�rdez�se
* `session`: Adott munkamenethez �llapotok be�ll�t�sa (pl. username, bejelentkez�s t�nye, etc. - ami minden lek�rdez�sn�l j�, ha el�rj�k)

R�gen: doGet() / doPost()

## Szerverek? ##

* Szervlet-kont�nerek (+JSP/JSTL)
* App. szerver: teljes J2EE stack (szervletek + EJB, JMS, CDI, JTA, etc.)

Tonn�nyi v�ltozat: Tomcat (referencia, j�t�k), Geronimo (Apache), GlassFish (Oracle, open source), JBoss (full EE stack, open source), Jetty (minim�l, embedded), WebLogic (a tough guy), ...

## Feladatok ##

1. Keressetek egy weboldalt, ami Java-alapon �zemel!
2. V�lasszatok egy tetsz�leges szerveralkalmaz�st (pl. Tomcat), t�lts�tek le, �ll�ts�tok be (`README`!), ind�ts�tok el.
3. �rjatok egy egyszer� JSP oldalt, amely 
4. T�rk�pezz�tek fel a p�ld�kat, k�rnyezetet!

## JSP Feladatok ##

1. K�sz�ts egy egyszer� JSP oldalt, amely egy minim�lis formon kereszt�l k�pes a sessionben id�zeteket t�rolni. Az oldal mindig �rja ki az elej�n a sessionh�z tartoz� azonos�t�t, azt, hogy �jonnan l�trehozott-e, a l�trehoz�s�nak d�tum�t, el�r�s�nek utols� d�tum�t, valamnint az eddig t�rolt id�zetek list�j�t egy felsorol�sban.
2. K�sz�ts egy egyszer� JSP oldalt, amely minden inform�ci�t ki�r egy t�bl�zatban a klinesr�l, ezt praktikusan a `request` objektumon kereszt�l �rheted el. Amit mindenk�pp �rjon ki az alkalmaz�s: a lek�rdez�s m�dj�t (`GET`/`POST`), a lek�rdez�s URI �s URL c�m�t, a context path �rt�k�t, a path inform�ci�t, a kapott *query stringet*, �s az azonos�t�si m�dot (*auth type*).

