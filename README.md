# mongoose
### mongoose
[官网](http://mongoosejs.com/)
[官方指南](http://mongoosejs.com/docs/guide.html)
[官方API文档](http://mongoosejs.com/docs/api.html)
- Mongdb数据库的基本概念
 + 可以有多个数据库
 + 一个数据库中有多个集合（表）
 + 一个集合可以有多个文档（表记录）
 + 文档结构很灵活，没有限制
 + MongoDB非常灵活，不需要像MySQL一样先创建数据库，表，设计表结构
   + 在这里只需要：当你插入数据的时候，只需要指定往哪个数据库的哪个集合操作就可以了
   + 一切都由MongoDB来帮你自动完成建库建表这件事情
 ```
 {
   qq: {
      users:[
        {name: '张三' ， age: 15},
        {name: '张四' ， age: 15},
        {name: '福之泉' ， age: 15},
        {name: '花生油' ， age: 15}
      ],
      products:[

      ],
      ...
   },
   taobao:{

   },
   baidu:{

   }
 }

 ```
- 起步
  + 安装
  ```
  npm i mongoose
  ```
  + 测试
  ```
  # 按照惯例 引入包
  var mongoose = require('mongoose')

  # 连接到数据库
  mongoose.connect('mongodb://localhost/test, {useMongoClient: true}')
  mongoose.Promise = global.Promise

  # 创建一个数据库模型
  # 实例化一个Cat
  var Cat = mongoose.Model('Cat', {name: String})
  var Kitty = new Cat({name: 'Zildjian'})

  # 持久化保存Kitty实例
  kitty.save(function(err){
    if(err){
      console.log(err)
    } else {
      console.log('meow')
    }
  })
  ```
- 官方指南 
  + 设计Schema，发布model

  ``` 
        var mongoose = require('mongoose')

        var Schema = mongoose.Schema

        //1.连接数据库
        //指定连接的数据库不需要存在，当你插入第一条数据之后就会自动创建出来
        mongoose.connect('mongodb://localhost/test')

        //2.设计集合(文档)结构（表结构）
        //字段名称就是表结构中的属性名称
        //值
        //约束的目的是为了保证数据的完整性，不要有脏数据

        var userSchema = new Schema({
          username : {
            type : String,
            required: true //必须有

          },
          password: {
            type: String,
            required: true
          },
          email: {
            type: String
          }

        })

        //3.将文档结构发布为模型
        //  mongoose.model方法就是用来将一个架构发布为model
        //  第一个参数：传入一个大写名词单数字符串用来表示你的数据库名称
        //             mongoose会自动将大写名词的字符串小写复数的集合名称
        //             例如这里的User最终会变成users集合名称
        //  第二个参数：架构Schema
        //  返回值： 模型构造函数
        var User = mongoose.model('User', userSchema)


        //4.当我们有了模型构造函数之后，就可以使用这个构造函数对Users集合中的的数据为所欲为了

  ```
  + 增加数据
  ```
      var admin = new User({
      username: 'admin',
      password: '123456',
      email: 'admin@admin.com'
    })

    admin.save(function(err , ret){
      if(err){
        console.log('保存失败')
      } else{
        console.log('保存成功')
        console.log(ret)
      }
    })
  ```
  + 查询所有
  ```
      User.find(function(err,ret){
          if(err){
            console.log('查询失败')
          } else {
            console.log(ret)
          }
        })
  ```
  + 按照条件查询所有
  ```
     User.find({
        username: 'admin'
      },function(err,ret){
        if(err){
          console.log('查询失败')
        } else {
          console.log(ret)
        }
      })
  ```
  + 按照条件查询单个
  ```
      User.findOne({
        username: 'admin'
      },function(err,ret){
        if(err){
          console.log('查询失败')
        } else {
          console.log(ret)
        }
      })
  ```
  + 删除数据
  ```
      User.remove({
        username: 'admin'
      },function(err, ret){
        if(err){
          console.log('删除失败')
        } else {
          console.log('删除成功')
          console.log(ret)
        }
      })
  ```
  + 更新数据
  ```
  User.findByIdAndUpdate('5d8233e8a48c80ce38fea3f4',{
      password: '123'
    },function(err,ret){
      if(err){
        console.log('更新失败')
      } else{
        console.log('更新成功')
      }
    })
  ```
  
