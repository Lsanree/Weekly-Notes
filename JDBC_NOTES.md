# JDBC_NOTES

标签（空格分隔）： 未分类

---

#JDBC与数据库
##1.加载驱动
##2.连接数据库
```
Connection connection=DriverManager.getConnection(dbur1, dbName, dbPassword);
```
##3.使用语句操作数据库
###（1）接口
####①statement接口
```
Connection connection=dbutil.getConnection(); //获取连接
     String sql="";
     Statement statement = connection.createStatement();
     statement.executeUpdate(sql);
```
####②PreparedStatement接口
```
Connection connection=dbutil.getConnection(); //获取连接
    	String sql="insert into t_book values(null,?,?,?,?)";
    	PreparedStatement pstmt =connection.prepareStatement(sql);
    	pstmt.setString(1,book.getBookName());
    	pstmt.executeUpdate();
```
####③CallableStatement接口:调用存储过程
```
private static String getBookNameById(int id)throws Exception{
		Connection connection=dbutil.getConnection();//获取连接
		String sql="call pro_getBookNameById(?,?)";
		CallableStatement cstmt=connection.prepareCall(sql);
		cstmt.setInt(1, id);//设置第一个参数值
		cstmt.registerOutParameter(2,Types.VARCHAR);//设置第二个参数值
		cstmt.execute();//执行操作
		String bookName=cstmt.getString("bn");//获取返回值
		dbutil.close(cstmt, connection);//关闭资源
		return bookName;
		
	}
```
###(2)结果集
####①形式一：具体值
```
Connection con = dbutil.getConnection();
		String sql = "select * from t_book";
		PreparedStatement pstmt = con.prepareStatement(sql);
		ResultSet rs = pstmt.executeQuery();
		while (rs.next()) {
			int id = rs.getInt(1);// 获取第一列的值ID
			String bookName = rs.getString(2);// 获取第二列值图书名
			Float price = rs.getFloat(3);// 获取第三列值图书价格
			String author = rs.getString(4);// 获取第四列值图书作者
			int bookTypeId = rs.getInt(5);// 获取第五列值图书类别
			System.out
					.println("图书编号" + id + "图书名称" + bookName + "图书价格" + price + "图书作者" + author + "图书类别" + bookTypeId);
			System.out.println("===================================");
		}
```
####②形式二：变量值
```
while (rs.next()) {
			int id = rs.getInt("id");// 获取第一列的值ID
			String bookName = rs.getString("bookName");// 获取第二列值图书名
			Float price = rs.getFloat("price");// 获取第三列值图书价格
			String author = rs.getString("author");// 获取第四列值图书作者
			int bookTypeId = rs.getInt("bookTypeId");// 获取第五列值图书类别
			System.out
					.println("图书编号" + id + "图书名称" + bookName + "图书价格" + price + "图书作者" + author + "图书类别" + bookTypeId);
			System.out.println("===================================");
		}
```
####③形式三:泛型
```
private static List<Book> listBook3() throws Exception {
		List<Book> bookList=new ArrayList();
		Connection con = dbutil.getConnection();
		String sql = "select * from t_book";
		PreparedStatement pstmt = con.prepareStatement(sql);
		ResultSet rs = pstmt.executeQuery();
		while (rs.next()) {
			int id = rs.getInt("id");// 获取第一列的值ID
			String bookName = rs.getString("bookName");// 获取第二列值图书名
			Float price = rs.getFloat("price");// 获取第三列值图书价格
			String author = rs.getString("author");// 获取第四列值图书作者
			int bookTypeId = rs.getInt("bookTypeId");// 获取第五列值图书类别
			Book book=new Book(id, bookName, author, price, bookTypeId);
			bookList.add(book);
		}
		return bookList;
	}
```
###3.数据
####(1)CLOB数据：字符型文本数据
#####①写入文本
```
File context = book.getContext();//获取数据
		InputStream inputstream = new FileInputStream(context);//引入输入流
		pstmt.setAsciiStream(5, inputstream, context.length());//设置第五个属性的值
```
#####②读取文本
```
ResultSet rs = pstmt.executeQuery();
            Clob c=rs.getClob("context");//获取文本
			String context=c.getSubString(1, (int)c.length());//输出文本
```			
####(2)BLOB数据：二进制文本数据
####①写入图片
```
File picture = book.getPicture();// 获取图片数据
		InputStream inputstream2 = new FileInputStream(picture);// 引入输入流
		pstmt.setBinaryStream(6, inputstream2, picture.length());//输入图片数据
```
#####②读取图片
```
Blob blob=rs.getBlob("picture");//获取图片数据
			FileOutputStream fileOutputStream=new FileOutputStream("e:/timg.jpg");//引入输出流
		    fileOutputStream.write(blob.getBytes(1,(int)blob.length()));//读取图片,1代表索引值
		    fileOutputStream.close();//关闭输出流
```
####(3)元数据：数据库基本信息
#####①DatabaseMetaD：获取数据库基本信息
```
Connection con=dbutil.getConnection();
		DatabaseMetaData dmd=con.getMetaData();//获取元数据
		System.out.println("数据库名称："+dmd.getDatabaseProductName());//获取数据库名称
		System.out.println("数据库版本："+dmd.getDatabaseMajorVersion()+"."+dmd.getDatabaseMinorVersion());//获取数据库版本
```
#####②ResultSetMetaData:获取ResultSet对象信息
```
Dbutil dbutil=new Dbutil();
		Connection con=dbutil.getConnection();
		String sql="select * from t_book";
		PreparedStatement pstmt=con.prepareStatement(sql);
		ResultSetMetaData rsmd=pstmt.getMetaData();//获取元数据结果集
		int num=rsmd.getColumnCount();//获取元数据总列数
		System.out.println("共有"+num+"列");
		for(int i=1;i<num;i++) {
			System.out.println(rsmd.getColumnName(i)+","+rsmd.getColumnTypeName(i));//获取指定列名称，指定列SQL类型名称
		}
```
###4.事务
####(1)事务特性
> ①原子性：事务最小单元，必须同时成功或失败
> ②一致性：数据库操作前后一致的，如果事务失败则回到原始状态
> ③持久性：事务完成后，对系统影响是持久的，即便系统故障也可保持
> ④隔离性：多事物同时进行且无法访问，事务最终操作时，才可看到结果
```
private static Dbutil dbutil=new Dbutil();
	//转出
	private static void outCount(Connection con,String accountName,int account )throws Exception{
		String sql="update t_account set accountBalance=accountBalance-? where accountName=?";
				PreparedStatement pstmt=con.prepareStatement(sql);
		pstmt.setInt(1, account);
		pstmt.setString(2, accountName);
		pstmt.executeUpdate();
	}
	//转入
	private static void inCount(Connection con,String accountName,int account )throws Exception{
		String sql="update t_account set accountBalance=accountBalance+? where accountName=?";
				PreparedStatement pstmt=con.prepareStatement(sql);
		pstmt.setInt(1, account);
		pstmt.setString(2, accountName);
		pstmt.executeUpdate();
	}
```
####(2)事务处理
#####①取消自动提交
```
con.setAutoCommit(false);//取消自动提交
```
#####②回滚
```
con.rollback(sp);//回滚
```
#####③提交事务
```
con.commit();//提交事务
```
####(3)保存点
```
SavePoint sp=con.setSavePoint;
```
##4.关闭数据连接，释放资源
```
public void close(Statement statement,Connection connection)throws Exception {
		if(statement!=null) {
			statement.close();
			if (connection!=null) {
				connection.close();
			}
		}
```		




