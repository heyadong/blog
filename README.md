<h3>这是一个用FLask 搭建的微电影网站</h3>

day1 2018-3-20：


day4 2018-3-22
<h3>自定义404页面：</h3>

注意在app 的 __init__ 文件里定义错误处理的路由：方式如下：



      @app.errorhandler(404)
      def page_not_found(error):
          return render_template('404.html')
    

<h3>后台管理页面搭建：</h3>

flask 蓝图flask.Blueprint 蓝图可以使app各模块分离，使程序结构更加清晰 容易维护

蓝图定义：

 admin __init__ 下定义：
 
 admin = Blueprint('admin', __name__)
 
 在app __init__ 注册 app.register_blueprint(admin, url_prefix="/admin")
 
 注意 url_prefix 参数 将使admin 的访问地址变为 localhost:5000/admin
 
 因此可以使用url_prefix 动态的创建路由
 
 蓝图定以后 路由的定义为@admin.route('/')
 
day4 2018-3-23

完成了网站前后台管理页面的搭建

day5 2018-3-26
<h3> 登陆的表单验证和密码验证</h3>

1、在models的Admin模型下 定义密码验证的方法：

werkzeug.security 中有 generate_password_hash()和 check_password_hash（）两个方法

generate_password_hash()生成密码的hash值字符串

check_password_hash(a,b) 比较两个值的hash值是否相同，返回True,False

使用flask_wtf 定义表单。

 ```
    from flask_wtf inmport FlaskForm
    from wtforms import StringField, SubmitField, PasswordField
    # 表单验证
    from wtforms.validators import Datarequired, ValidationError
    class LoginForm(FlaskForm):
      account = StringField()
      password = PasswordField()
  ```
      
      
      
StringFeild()都可以传入关键字参数 :

validators=[]   验证消息

render_kw{} 表单其他信息css样式

1.前端渲染表单提示消息使用，form.account.errors

```
  {% for error in form.account.errors %}
  {% endfor %}
```
     
     
2.flask消息的闪现，提示密码输入错误。前端使用for循环，
  flash（）用法
  
  flask.flash(message，kindofmsg) 第二个参数表示消息的种类，

```
  {{
  {% for message in get_flashed_messages(category_filter['ok']) %}
  {{ message}}
  {% endfor %} }}
```
day6 2018-3-27
Flask_SQLAlchemy 使用ORM的增删改查：



### 增加
    
 ```
  movie = Movie(id=id,title=title)
  db.session.add(movie)
  db.session.commit()
    
   
   Insert into movie(id, title) values(id,title) 
 ```
    
 ### 删除
    
  ```
   movie= Movie.query.filter_by(id=moive_id).first()
   db.session.delete()
   db.session.commit()
   ''' delete from movie where id=movie_id '''
  ```
    
### 修改
    
### 查询
```
    movie.query.filter_by(id=movie_id).first()
```
    
### 模糊查询
    
 ```
  movie.query.filter(Movie.title.ilile("%name%").order_by().all()
  select * from movie where title like '%name%'
 ```
    
    
### 查询列
 ```
   movie.query.with_entities(movie.title).all() 
   返回的是tuple
    
    
  <h3>使用sqlalchemy分页</h3>  
 ```
day7 2018-4-11

```
User.query.oreder_by(user.add_time()).paginate(page=1,)
```


Jinja2 支持宏



