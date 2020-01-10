第一个shiro入门程序的开发步骤
1.在pom.xml文件中加入如下依赖
<!-- https://mvnrepository.com/artifact/org.apache.shiro/shiro-core -->
<dependency>
    <groupId>org.apache.shiro</groupId>
    <artifactId>shiro-core</artifactId>
    <version>1.2.2</version>
</dependency>
第二步:在resources目录下新建shiro.ini
[users]
admin=123456
test=000000
第三步：测试程序
@Test
    public void testHelloShiro()
    {
        //创建SecurityManager工厂对象
        Factory<SecurityManager> factory=new IniSecurityManagerFactory("classpath:shiro.ini");
        //获取SecurityManager对象
        SecurityManager securtyManager=factory.getInstance();
        //通过SecurtiyUtils设置securtyManager
        SecurityUtils.setSecurityManager(securtyManager);
        //获取Subject主体对象
        Subject subject=SecurityUtils.getSubject();
        //创建UserPassword
        UsernamePasswordToken token=new UsernamePasswordToken("admin1","123456");
        //通过subject中的login完成登陆
        try {
            subject.login(token);
            if(subject.isAuthenticated()){
                System.out.println("登陆成功!");
            }
        } catch (AuthenticationException e) {
            e.printStackTrace();
            System.out.println("登陆失败！");
        }

    }
UnknownAccountException：没有账户错误
IncorrectCredentialsException:密码错误