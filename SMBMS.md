## SMBMS

## 复制Tomcat

直接将文件夹复制一份，修改配置端口号即可

![](https://img-blog.csdnimg.cn/3568b597b7af4c1a8e403a93774ecf5b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

数据库：

![](https://img-blog.csdnimg.cn/b564a6b1069b4057b3fd033fb5b4bbe2.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

**项目如何搭建？**

考虑是否使用Maven？使用就需要依赖，否则需要手动导入jar包

## 项目搭建

1. 搭建一个 Maven web 项目

2. 配置Tomcat

3. 测试项目是否能够成功运行

4. 导入项目中需要的jar包

   servlet，jsp，mysql驱动，jstl，standard...

5. 创建项目包结构

   ![](https://img-blog.csdnimg.cn/2ab6892ac7d148fe86bacd74175a4283.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

6. 编写实体类（方到pojo包下）

   ORM映射：表-类映射

   对应数据库字段建立实体类属性和get set方法，以下代码片段省略了get set

   ```java
   package com.Sucker.pojo;
   
   import java.util.Date;
   
   public class User {
       private Integer id; //id
       private String userCode; //用户编码
       private String username; //用户名称
       private String userPassword; //用户密码
       private Integer gender; //性别
       private Date birthday; //生日
       private String phone; //电话
       private String address; //地址
       private Integer userRole; //用户角色
       private Integer createBy; //创建者
       private Date creationDate; //创建时间
       private Integer modifyBy; //更新者
       private Date modifyDate; //更新时间
   
       private Integer age; //年龄
       private String userRoleName; //用户角色名称
   
       public Integer getAge() {
           Date date = new Date();
           Integer age = date.getYear() - birthday.getYear();
           return age;
       }
       public void setAge(Integer age) {
           this.age = age;
       }
       public String getUserRoleName() {
           return userRoleName;
       }
       public void setUserRoleName(String userRoleName) {
           this.userRoleName = userRoleName;
       }
   
   }
   ```

7. 编写基础公共类

   - 数据库配置文件

     ![](https://img-blog.csdnimg.cn/919916ed91334142b1484500d96502ad.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

   - 编写数据库的公共类
   
     ```java
     package com.Sucker.dao;
     
     import java.io.IOException;
     import java.io.InputStream;
     import java.sql.*;
     import java.util.Properties;
     
     //操作数据库的公共类
     public class BaseDao {
     
         private static String driver;
         private static String url;
         private static String username;
         private static String password;
     
         //静态代码块，类加载的时候就初始化
         static{
             Properties properties = new Properties();
             //通过类加载器读取对应资源
             InputStream is = BaseDao.class.getClassLoader().getResourceAsStream("db.properties");
     
             try {
                 properties.load(is);
             } catch (IOException e) {
                 e.printStackTrace();
             }
     
             driver = properties.getProperty("driver");
             url = properties.getProperty("url");
             username = properties.getProperty("username");
             password = properties.getProperty("password");
         }
     
         //获取数据库的连接
         public static Connection getConnection(){
             Connection connection = null;
             try {
                 Class.forName(driver);
                 connection = DriverManager.getConnection(url, username, password);
             } catch (Exception e) {
                 e.printStackTrace();
             }
             return connection;
         }
     
         //编写查询公共类
         public static ResultSet execute(Connection connection,String sql,Object[] params,ResultSet resultSet,PreparedStatement preparedStatement) throws SQLException {
             //预编译的sql，后面直接执行就行不用传参
             preparedStatement = connection.prepareStatement(sql);
     
             for (int i = 0; i < params.length; i++) {
                 preparedStatement.setObject(i+1,params[i]);//占位符从1开始
             }
     
             resultSet = preparedStatement.executeQuery(sql);
             return resultSet;
         }
     
         //编写增删改公共方法
         public static int execute(Connection connection,String sql,Object[] params,PreparedStatement preparedStatement) throws SQLException {
             //预编译的sql，后面直接执行就行不用传参
             preparedStatement = connection.prepareStatement(sql);
     
             for (int i = 0; i < params.length; i++) {
                 preparedStatement.setObject(i+1,params[i]);//占位符从1开始
             }
     
             int updateRows = preparedStatement.executeUpdate();
             return updateRows;
         }
     
         //释放资源
         public static boolean closeResource(Connection connection,PreparedStatement preparedStatement,ResultSet resultSet){
             boolean flag = true;
     
             if (resultSet!=null){
                 try {
                     resultSet.close();
                     //GC回收
                     resultSet=null;
                 } catch (SQLException throwables) {
                     throwables.printStackTrace();
                     flag=false;
                 }
             }
     
             if (preparedStatement!=null){
                 try {
                     preparedStatement.close();
                     //GC回收
                     preparedStatement=null;
                 } catch (SQLException throwables) {
                     throwables.printStackTrace();
                     flag=false;
                 }
             }
     
             if (connection!=null){
                 try {
                     connection.close();
                     //GC回收
                     connection=null;
                 } catch (SQLException throwables) {
                     throwables.printStackTrace();
                     flag=false;
                 }
             }
             return flag;
         }
     
     
     }
     ```
   
   - 编写字符编码过滤器
   
     ```java
     package com.Sucker.filter;
     
     import javax.servlet.*;
     import java.io.IOException;
     
     public class CharacterEncodingFilter implements Filter{
     
         public void init(FilterConfig filterConfig) throws ServletException {
     
         }
     
         public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
             servletRequest.setCharacterEncoding("utf-8");
             servletResponse.setCharacterEncoding("utf-8");
     
             filterChain.doFilter(servletRequest,servletResponse);
         }
     
         public void destroy() {
     
         }
     }
     ```
   
     配置web.xml
   
     ```xml
     <!--    字符编码过滤器-->
         <filter>
             <filter-name>CharacterEncodingFilter</filter-name>
             <filter-class>com.Sucker.filter.CharacterEncodingFilter</filter-class>
         </filter>
         <filter-mapping>
             <filter-name>CharacterEncodingFilter</filter-name>
             <url-pattern>/*</url-pattern>
         </filter-mapping>
     ```
   
8. 导入静态资源到webapp目录下

## 登录功能实现

![](https://img-blog.csdnimg.cn/a427756fd2a54804b626dee32802780e.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

1. 编写前端页面

2. 设置首页

   ```xml
   <!--    设置欢迎页面-->
       <welcome-file-list>
           <welcome-file>login.jsp</welcome-file>
       </welcome-file-list>
   ```

3. 编写Dao层用户登录的接口

   ```java
   public interface UserDao {
       //得到登录的用户
       public User getLoginUser(Connection connection,String userCode) throws SQLException;
   
   }
   ```

4. 编写UserDao接口的实现类

   ```java
   public class UserDaoImpl implements UserDao{
       //得到要登录的用户
       public User getLoginUser(Connection connection, String userCode) throws SQLException {
   
           PreparedStatement pstm = null;
           ResultSet rs = null;
           User user = null;
   
           if (connection!=null){
               String sql = "select * from smbms_user where userCode=?";//用？保证安全，预编译的sql
               Object[] params = {userCode};
   
               rs = BaseDao.execute(connection, pstm, rs, sql, params);
   
               if (rs.next()) {
                   user = new User();
                   user.setId(rs.getInt("id"));
                   user.setUserCode(rs.getString("userCode"));
                   user.setUserName(rs.getString("userName"));
                   user.setUserPassword(rs.getString("userPassword"));
                   user.setGender(rs.getInt("gender"));
                   user.setBirthday(rs.getDate("birthday"));
                   user.setPhone(rs.getString("phone"));
                   user.setAddress(rs.getString("address"));
                   user.setUserRole(rs.getInt("userRole"));
                   user.setCreateBy(rs.getInt("createBy"));
                   user.setCreationDate(rs.getDate("creationDate"));
                   user.setModifyBy(rs.getInt("modifyBy"));
                   user.setModifyDate(rs.getDate("modifyDate"));
               }
               BaseDao.closeResource(null,pstm,rs);//连接先不关
   
           }
           return user;
       }
   
   }
   ```

5. 业务层接口

   ```java
   public interface UserService {
       //用户登录
       public User login(String userCode,String password);
   }
   ```

6. 业务层实现类

   ```java
   public class UserServiceImpl implements UserService{
   
       //业务层都会调用Dao层，所以我们要引入Dao层
       private UserDao userDao;
       public UserServiceImpl(){
           userDao = new UserDaoImpl();
       }
   
       public User login(String userCode, String password) {
           Connection connection = null;
           User user = null;
   
           try {
               connection = BaseDao.getConnection();
               //通过业务层调用对应的具体的数据库操作
               user = userDao.getLoginUser(connection, userCode);
           } catch (SQLException throwables) {
               throwables.printStackTrace();
           }finally {
               BaseDao.closeResource(connection,null,null);
           }
           return user;
       }
   
   }
   ```

7. 编写Servlet

   导入login.jsp到webapp目录下

   增加jsp包到webapp下，建立common文件夹，里面导入foot.jsp与head.jsp

   jsp包下导入frame.jsp作为登录成功首页

    转发回登录页面,顺带提示它，用户名或密码错误

   ```java
   public class LoginServlet extends HttpServlet {
   
       //Servlet : 控制层，调用业务层代码
   
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
   
           System.out.println("LoginServlet--start...");
   
           //获取用户名与密码
           String userCode = req.getParameter("userCode");
           String userPassword = req.getParameter("userPassword");//这里要与前端对应
   
           //和数据库中的密码做对比，调用业务层;
           UserService userService = new UserServiceImpl();
           User user = userService.login(userCode, userPassword); //这里已经把登录的人查出来了
   
           if (user!=null&&user.getUserPassword().equals(userPassword)){ //查有此人
               //将用户的信息放到Session中
               req.getSession().setAttribute(Constants.USER_SESSION,user);
               //跳转到主页
               resp.sendRedirect("jsp/frame.jsp");
           }else { //查无此人
               //转发回登录页面,顺带提示它，用户名或密码错误
               req.setAttribute("error","用户名或密码不正确");
               req.getRequestDispatcher("login.jsp").forward(req,resp);//使用转发能携带参数
           }
   
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           doGet(req, resp);
       }
   }
   ```

8. 注册servlet

   此处参考login.jsp中提交表单的路径为login.do

   ```xml
       <servlet>
           <servlet-name>LoginServlet</servlet-name>
           <servlet-class>com.Sucker.servlet.user.LoginServlet</servlet-class>
       </servlet>
       <servlet-mapping>
           <servlet-name>LoginServlet</servlet-name>
           <url-pattern>/login.do</url-pattern>
       </servlet-mapping>
   ```

9. 测试是否成功

## 登录功能优化

### 注销功能：

思路：移除Session，返回登录页面

```java
public class LogoutServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //移除用户的Constants.USER_SESSION
        req.getSession().removeAttribute(Constants.USER_SESSION);
        resp.sendRedirect(req.getContextPath()+"/login.jsp");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

同理参照head.jsp里面退出的路径

```xml
    <servlet>
        <servlet-name>LogoutServlet</servlet-name>
        <servlet-class>com.Sucker.servlet.user.LogoutServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>LogoutServlet</servlet-name>
        <url-pattern>/jsp/logout.do</url-pattern>
    </servlet-mapping>
```

**路径问题**
重定向因为是从客户端发来的，所以只知道发到那个服务器，不知道发给那个项目，所以重定向的"/"表示"http:服务器ip:8080/"
请求转发因为服务器内部自己转发，因此知道发给那个项目，所以请求转发的"/"表示"http:服务器ip:8080/项目名/"
重定向没有"/"表示在当前目录，请求转发没有"/"表示相对于当前资源的相对路径

重点参考：[(13条消息) JavaWeb中“重定向”和“请求转发”的路径问题_Kaiter的博客-CSDN博客](https://blog.csdn.net/qq_40761746/article/details/105441924)

### 登录拦截优化

将error.jsp导入到webapp目录下

编写一个过滤器，并注册

```java
public class SysFilter implements Filter {
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    public void doFilter(ServletRequest req, ServletResponse resp, FilterChain filterChain) throws IOException, ServletException {
        HttpServletRequest request = (HttpServletRequest) req;
        HttpServletResponse response = (HttpServletResponse) resp;

        //过滤器，从Session中获取用户，
        User user = (User) request.getSession().getAttribute(Constants.USER_SESSION);

        if (user==null){//已经被移除或注销，或未登录
            response.sendRedirect(request.getContextPath()+"/error.jsp");
        }else{
            filterChain.doFilter(req,resp);//注意这里要用原来的
        }

    }

    public void destroy() {

    }
}
```

```xml
<!--    用户登录过滤器-->
    <filter>
        <filter-name>SysFilter</filter-name>
        <filter-class>com.Sucker.filter.SysFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>SysFilter</filter-name>
        <url-pattern>/jsp/*</url-pattern>
    </filter-mapping>
```

测试

## 密码修改

### 密码修改

1. 导入前端素材，看head.jsp里面的路径

   ```jsp
   <li><a href="${pageContext.request.contextPath }/jsp/pwdmodify.jsp">密码修改</a></li>
   ```

2. 写项目，建议从底层往上写

   ![](https://img-blog.csdnimg.cn/2e866431ffc447b39cd5e80e0b2a4eb0.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

3. UserDao 接口

   ```java
   public interface UserDao {
   
       //得到登录的用户
       public User getLoginUser(Connection connection,String userCode) throws SQLException;
   
       //修改当前用户密码
       public int updatePwd(Connection connection,int id,String password) throws SQLException;
   
   }
   ```

4. UserDao 接口实现类

   ```java
   //修改当前用户的密码
   public int updatePwd(Connection connection, int id, String password) throws SQLException {
   
       PreparedStatement pstm = null;
       int execute = 0;
   
       if (connection!=null){
           String sql = "update smbms_user set userPassword = ? where id = ?";
           Object[] params = {password,id};
           execute = BaseDao.execute(connection, pstm,sql, params);
           BaseDao.closeResource(null,pstm,null);
       }
       return execute;
   }
   ```

5. UserService接口

   ```java
   public interface UserService {
       //用户登录
       public User login(String userCode,String password);
   
       //根据用户ID修改密码
       public boolean updatePwd(int id,String pwd);
   }
   ```

6. UserService接口实现类

   ```java
   public boolean updatePwd(int id, String pwd) {
       Connection connection = null;
       boolean flag = false;
       try {
           connection = BaseDao.getConnection();
           //修改密码
           if (userDao.updatePwd(connection,id,pwd)>0) flag=true;
       } catch (SQLException throwables) {
           throwables.printStackTrace();
       }finally {
           BaseDao.closeResource(connection,null,null);
       }
       return flag;
   }
   ```

7. 编写能实现复用的Servlet，实现复用需要提取出方法

   ```java
   package com.Sucker.servlet.user;
   
   //实现Servlet复用
   public class UserServlet extends HttpServlet {
   
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           String method = req.getParameter("method");
           if (method!=null&&method.equals("savepwd")){
               this.updatePwd(req,resp);
           }
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           doGet(req, resp);
       }
   
       public void updatePwd(HttpServletRequest req, HttpServletResponse resp){
           //从Session里面拿ID；
           Object o = req.getSession().getAttribute(Constants.USER_SESSION);
           String newpassword = req.getParameter("newpassword");
           boolean flag = false;
   
           if (o!=null && (!StringUtils.isNullOrEmpty(newpassword)) ){
               UserService userService = new UserServiceImpl();
               flag = userService.updatePwd(((User) o).getId(), newpassword);
               if (flag){
                   req.setAttribute("message","修改密码成功，请退出使用新密码登录");
                   //密码修改成功，移除当前Session
                   req.getSession().removeAttribute(Constants.USER_SESSION);
               }else{
                   req.setAttribute("message","修改密码失败");
               }
   
           }else{
               req.setAttribute("message","新密码有误");
           }
   
           try {
               req.getRequestDispatcher("pwdmodify.jsp").forward(req,resp);
           } catch (ServletException e) {
               e.printStackTrace();
           } catch (IOException e) {
               e.printStackTrace();
           }
       }
   
   }
   ```

   ```xml
   <!--    根据前端页面（pwdmodify.jsp）看url-->
       <servlet>
           <servlet-name>UserServlet</servlet-name>
           <servlet-class>com.Sucker.servlet.user.UserServlet</servlet-class>
       </servlet>
       <servlet-mapping>
           <servlet-name>UserServlet</servlet-name>
           <url-pattern>/jsp/user.do</url-pattern>
       </servlet-mapping>
   ```

### 优化密码修改（Ajax）

1. 使用阿里巴巴 fastjson

   ```xml
       <dependency>
         <groupId>com.alibaba</groupId>
         <artifactId>fastjson</artifactId>
         <version>1.2.61</version>
       </dependency>
   ```

2. 实现Servlet复用

   ```java
   public class UserServlet extends HttpServlet {
   
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           String method = req.getParameter("method");
           if (method!=null&&method.equals("savepwd")){
               this.updatePwd(req,resp);
           }else if (method!=null&&method.equals("pwdmodify")){
               this.pwdModify(req,resp);
           }
       }
       
           //验证旧密码,session中有用户的密码
       public void pwdModify(HttpServletRequest req, HttpServletResponse resp){
           //从Session里面拿password；
           Object o = req.getSession().getAttribute(Constants.USER_SESSION);
           String oldpassword = req.getParameter("oldpassword");
   
           //万能的Map : 结果集
           Map<String,String> resultMap = new HashMap<String,String>();
   
           //对照pwdmodify.js中的ajax里的参数
           if (o==null){ //Session失效，过期
               resultMap.put("result","sessionerror");
           }else if (StringUtils.isNullOrEmpty(oldpassword)){//输入的密码为空
               resultMap.put("result","error");
           }else {
               String userPassword = ((User) o).getUserPassword();
               if (oldpassword.equals(userPassword)){
                   resultMap.put("result","true");
               }else{
                   resultMap.put("result","false");
               }
           }
   
           try {
               resp.setContentType("application/json");//设置为json类型
               PrintWriter writer = resp.getWriter();
               //JSONArray 阿里巴巴的JSON工具类，转换格式用
               /*
               resultMap = ["result","sessionerror","result","error"]
               Json格式 = {key : value}
                */
               writer.write(JSONArray.toJSONString(resultMap));
               writer.flush();
               writer.close();
   
           } catch (IOException e) {
               e.printStackTrace();
           }
   
   
       }
   }
   ```

   pwdmodify.js中的部分ajax

   ```js
   	oldpassword.on("blur",function(){
   		$.ajax({
   			type:"GET",
   			url:path+"/jsp/user.do",
   			data:{method:"pwdmodify",oldpassword:oldpassword.val()}, //Ajax传递的参数
   			dataType:"json", //主流开发都是用JSON实现前后端
   			success:function(data){
   				if(data.result == "true"){//旧密码正确
   					validateTip(oldpassword.next(),{"color":"green"},imgYes,true);
   				}else if(data.result == "false"){//旧密码输入不正确
   					validateTip(oldpassword.next(),{"color":"red"},imgNo + " 原密码输入不正确",false);
   				}else if(data.result == "sessionerror"){//当前用户session过期，请重新登录
   					validateTip(oldpassword.next(),{"color":"red"},imgNo + " 当前用户session过期，请重新登录",false);
   				}else if(data.result == "error"){//旧密码输入为空
   					validateTip(oldpassword.next(),{"color":"red"},imgNo + " 请输入旧密码",false);
   				}
   			},
   			error:function(data){
   				//请求出错
   				validateTip(oldpassword.next(),{"color":"red"},imgNo + " 请求错误",false);
   			}
   		});
   ```

## 用户管理实现

思路：

![](https://img-blog.csdnimg.cn/130b34cec4e5491c90f4e19affbaf740.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

1. 导入分页的工具类（PageSuppot.java）

2. 用户列表页面导入

   userlist.jsp，在这其中还能看到还需要rollpage.jsp

### 获取用户数量

1. UserDao接口

   ```java
   //查询用户总数
   public int getUserCount(Connection connection,String username,int userRole) throws SQLException;
   ```

2. UserDaoImpl实现类

   ```java
   //根据用户名或角色 查询用户总数【最难理解的SQL】
   public int getUserCount(Connection connection, String username, int userRole) throws SQLException {
   
       PreparedStatement preparedStatement = null;
       ResultSet rs = null;
       int count = 0;
   
       if (connection!=null){
           StringBuffer sql = new StringBuffer();
           sql.append("select count(1) as count from smbms_user u ,smbms_role r where u.userRole=r.id");
           ArrayList<Object> list = new ArrayList<Object>();//存放参数
   
           if (!StringUtils.isNullOrEmpty(username)) {
               sql.append(" and u.username like ?");
               list.add("%"+username+"%");//index = 0;这里是为了符合sql要求，传进？的参数需要带两个%
           }
   
           if (userRole>0) {
               sql.append(" and u.userRole = ?");
               list.add(userRole);//index = 1
           }
   
           //把list转换为数组
           Object[] params = list.toArray();
   
           System.out.println("UserDaoImpl->getUserCount:"+sql.toString());
   
           rs = BaseDao.execute(connection, preparedStatement, rs, sql.toString(), params);//返回查出来的结果集
   
           if (rs.next()){
               count = rs.getInt("count");//因为前面取了别名叫count，所以结果集中是count
           }
           BaseDao.closeResource(null,preparedStatement,rs);
   
       }
       return count;
   }
   ```

3. UserService接口

   ```java
   //查询记录数
   public int getUserCount(String username,int userRole);
   ```

4. UserServiceImpl

   可以用junit测试单元

   ```java
       @Test
       public void test(){
           UserServiceImpl userService = new UserServiceImpl();
           int userCount = userService.getUserCount(null, 1);
           System.out.println(userCount);
       }
   ```

   ```java
   //查询记录数
   public int getUserCount(String username, int userRole) {
   
       Connection connection = null;
       int count = 0;
       try {
           connection = BaseDao.getConnection();
           count = userDao.getUserCount(connection, username, userRole);
   
       } catch (SQLException throwables) {
           throwables.printStackTrace();
       }finally {
           BaseDao.closeResource(connection,null,null);
       }
       return count;
   }
   ```


### 获取用户列表

1. UserDao接口

   ```java
   //获取用户列表  通过条件查询-userlist
   public List<User> getUserList(Connection connection, String userName, int userRole, int currentPageNo, int pageSize) throws Exception;
   ```

2. UserDaoImpl实现类

   ```java
       //获取用户列表  通过条件查询-userlist
       public List<User> getUserList(Connection connection, String username, int userRole, int currentPageNo, int pageSize) throws Exception {
   
           PreparedStatement preparedStatement = null;
           ResultSet rs = null;
           List<User> userList = new ArrayList<User>();
           if (connection!=null){
               StringBuffer sql = new StringBuffer();
               sql.append("select u.*,r.roleName as userRoleName from smbms_user u ,smbms_role r where u.userRole = r.id");
               List<Object> list = new ArrayList<Object>();//存放参数
               if (!StringUtils.isNullOrEmpty(username)) {
                   sql.append(" and u.username like ?");
                   list.add("%"+username+"%");//index = 0;这里是为了符合sql要求，传进？的参数需要带两个%
               }
               if (userRole>0) {
                   sql.append(" and u.userRole = ?");
                   list.add(userRole);//index = 0;这里是为了符合sql要求，传进？的参数需要带两个%
               }
   
               //在数据库中，分页使用 limit  startIndex，pageSize；总数
               //当前页起始数据下标 = （当前页号-1）*页面大小
               //0，5   1（第一页）  0（起始下标） 01234
               //5，5   2           5           56789
               //10，5  3           10
   
               sql.append(" order by creationDate DESC limit ?,?");
               currentPageNo = (currentPageNo-1)*pageSize;
               list.add(currentPageNo);
               list.add(pageSize);
   
               Object[] params = list.toArray();
               System.out.println("sql--->"+sql.toString());
               rs = BaseDao.execute(connection, preparedStatement, rs, sql.toString(), params);
   
               while (rs.next()) {
                   User user = new User();
                   user.setId(rs.getInt("id"));
                   user.setUserCode(rs.getString("userCode"));
                   user.setUserName(rs.getString("userName"));
                   user.setGender(rs.getInt("gender"));
                   user.setBirthday(rs.getDate("birthday"));
                   user.setPhone(rs.getString("phone"));
                   user.setUserRole(rs.getInt("userRole"));
                   user.setUserRoleName(rs.getString("userRoleName"));
                   userList.add(user);
               }
               BaseDao.closeResource(null,preparedStatement,rs);
           }
           return userList;
       }
   ```

3. UserService接口

   ```java
   //根据条件查询用户列表
   public List<User> getUserList(String queryUserName,int queryUserRole,int currentPageNo,int pageSize);
   ```

4. UserServiceImpl

   可以使用junit单元测试

   ```java
   @Test
   public void test(){
       UserServiceImpl userService = new UserServiceImpl();
       List<User> userList = userService.getUserList("系统管理员", 1, 1, 5);
       System.out.println(userList);//这里要去User类中加toString方法
   }
   ```

   ```java
   public List<User> getUserList(String queryUserName, int queryUserRole, int currentPageNo, int pageSize) {
       Connection connection = null;
       List<User> userList = new ArrayList<User>();
       System.out.println("queryUserName--->"+queryUserName);
       System.out.println("queryUserRole--->"+queryUserRole);
       System.out.println("currentPageNo--->"+currentPageNo);
       System.out.println("pageSize--->"+pageSize);
       try {
           connection = BaseDao.getConnection();
           userList = userDao.getUserList(connection,queryUserName,queryUserRole,currentPageNo,pageSize);
       } catch (Exception throwables) {
           throwables.printStackTrace();
       }finally {
           BaseDao.closeResource(connection,null,null);
       }
       return userList;
   }
   ```

### 获取角色列表

为了职责分明，可以把角色的操作单独放到一个包中，和pojo类对应。

![](https://img-blog.csdnimg.cn/27ecf481f8a84161b106d61ccb36abb6.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

1. RoleDao接口

   ```java
   public interface RoleDao {
       //获取角色列表
       public List<Role> getRoleList(Connection connection) throws SQLException;
   }
   ```

2. RoleDao接口实现类

   ```java
   //获取角色列表
   public List<Role> getRoleList(Connection connection) throws SQLException {
   
       PreparedStatement pstm = null;
       ResultSet rs = null;
       ArrayList<Role> roleList = new ArrayList<Role>();
   
       if (connection!=null){
           String sql = "select * from smbms_role";
           Object[] params = {};
           rs = BaseDao.execute(connection, pstm, rs, sql, params);
   
           while (rs.next()){
               Role role = new Role();
               role.setId(rs.getInt("id"));
               role.setRoleCode(rs.getString("roleCode"));
               role.setRoleName(rs.getString("roleName"));
               roleList.add(role);
           }
           BaseDao.closeResource(null,pstm,rs);
       }
       return roleList;
   }
   ```

3. UserService接口

   ```java
   public interface RoleService {
       //获取角色列表
       public List<Role> getRoleList();
   }
   ```

4. UserService接口实现类

   ```java
   public class RoleServiceImpl implements RoleService{
   
       //引入Dao
       private RoleDao roleDao;
       public RoleServiceImpl(){
           roleDao = new RoleDaoImpl();
       }
   
       //获取角色列表
       public List<Role> getRoleList() {
   
           Connection connection =null;
           List<Role> roleList = null;
           try {
               connection = BaseDao.getConnection();
               roleList = roleDao.getRoleList(connection);
           } catch (SQLException throwables) {
               throwables.printStackTrace();
           }finally {
               BaseDao.closeResource(connection,null,null);
           }
           return roleList;
       }
   }
   
   ```

### 用户显示的Servlet

实现servlet复用，在UserServlet中增加判断，通过前端页面看出method参数

```java
//实现Servlet复用
public class UserServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String method = req.getParameter("method");
        if (method!=null&&method.equals("savepwd")){
            this.updatePwd(req,resp);
        }else if (method!=null&&method.equals("pwdmodify")){
            this.pwdModify(req,resp);
        }else if (method!=null&&method.equals("query")){
            this.query(req,resp);
        }
    }
```

1. 获取用户前端的数据（查询）
2. 判断请求是否需要执行，看参数的值判断
3. 实现分页
4. 用户列表展示
5. 返回前端

```java
//重点难点：用户管理
public void query(HttpServletRequest req, HttpServletResponse resp){

    //查询用户列表

    //从前端获取数据：userlist.jsp(看其中需要的name:)
    String queryUserName = req.getParameter("queryName");
    String temp = req.getParameter("queryUserRole");
    String pageIndex = req.getParameter("pageIndex");
    int queryUserRole = 0;//设置默认为0

    //获取用户列表
    UserServiceImpl userService = new UserServiceImpl();
    List<User> userList = null; //以下操作为设置参数

    //第一次走这个请求，一定是第一页，页面大小固定
    int pageSize = 5; //可以把这个写到配置文件中，方便后期修改
    int currentPageNo = 1;

    if (queryUserName==null) queryUserName = "";//如果是空，后面动态sql查询的时候是不会进入if判断故直接查询出所有数据
    if (temp!=null && !temp.equals("")) queryUserRole = Integer.parseInt(temp);//给查询赋值 0,1,2,3
    if(pageIndex!=null){
        currentPageNo = Integer.parseInt(pageIndex);
    }

    //获取用户总数 (分页：上一页，下一页的情况)
    int totalCount = userService.getUserCount(queryUserName, queryUserRole);
    //总页数支持  这里是为了算出总页数
    PageSupport pageSupport = new PageSupport();
    pageSupport.setCurrentPageNo(currentPageNo);
    pageSupport.setPageSize(pageSize);
    pageSupport.setTotalCount(totalCount);//此处已经调用设置总页数的算法

    int totalPageCount = pageSupport.getTotalPageCount(); // 得到总页数

    //控制首页和尾页
    //如果页面要小于1了，就显示第一页的东西
    if (currentPageNo < 1){
        currentPageNo = 1;
    }else if (currentPageNo>totalPageCount){//当前页面大于了最后一页
        currentPageNo = totalPageCount;
    }

    //获取用户列表展示
    userList = userService.getUserList(queryUserName, queryUserRole, currentPageNo, pageSize);
    req.setAttribute("userList",userList);

    RoleServiceImpl roleService = new RoleServiceImpl();
    List<Role> roleList = roleService.getRoleList();
    req.setAttribute("roleList",roleList);
    req.setAttribute("totalCount",totalCount);
    req.setAttribute("currentPageNo",currentPageNo);
    req.setAttribute("totalPageCount",totalPageCount);
    req.setAttribute("queryUserName",queryUserName);
    req.setAttribute("queryUserRole",queryUserRole);

    //返回前端
    try {
        req.getRequestDispatcher("userlist.jsp").forward(req,resp);
    } catch (ServletException e) {
        e.printStackTrace();
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

![](https://img-blog.csdnimg.cn/4653428a97444e6198efdeaa9cc59103.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzUxNTcyNzE0,size_16,color_FFFFFF,t_70)

其他两个功能类似思路

