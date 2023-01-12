# サーブレットクラスの実行方法

サーブレットクラスを実行するには、ブラウザでサーブレットクラスのURLを指定してリクエストします。 サーブレットクラスのURLは、次の形式で指定します。　　　　＝＝＝＞　http://<サーバ名>/<アプリケーション名>/<URLパターン> サーブレットクラスはURLパターンを設定しないとリクエストして実行することができません。

## URLパターンの設定
アノテーションで付加された情報は、外部ツールに読み込ませることが可能です。
サーブレットクラスに、@WebServletアノテーションを加えると、アプリケーションサーバがそれを読み取り、URLパターン設定を行います。（めっちゃ重要じゃん）
### UR



# DAO パターンとは
 データベース操作（テーブルに対する検索、追加、更新、削除など）をたんんとうするクラスを用意して、データベースに修正が必要なときでも、容易に修正ができるようにする手法。
 
 - メリット：
   - データベースに変更があっても、そのデータベースを利用するクラスたちは修正する必要がなくなるので、ソースコードの保守性が高くなる。
   - データベースの知識がない開発者でもDAOを介してデータベースを利用することが可能になるので、開発の効率も上がる。
 
 - 見た目: DAOパターンを用いると、データベースを利用するクラスからJDBCプログラム特有のコードがなくなる。（スッキリ！）
 # EMPLOYEE テーブルを担当する DAO
 
 ```Java
 package dao;
 
 import java.sql.Connection;
 import java.sql.DriverManager;
 import java.sql.PreparedStatement;
 import java.sql.resultSet;
 import java.sql.SQLException;
 import java.util.ArrayList;
 import java.util.List;
 import moder.Employee;
 
 public class EmployeeDAO{
 //データベース接続に使用する情報
 private final String JDBC_URL = "jdbc:h2:tcp://localhost/~/example;
 private final String DB_USER = "sa" ;
 private final String DB_PASS = "";
 
 public List<Employee> findAll(){
 List<Employee> empList = new ArrayList<>();
 //データベースへ接続
 try{Connection conn = DriveerManager.getConnection{JDBC_URL, DB_USER, DB_PASS)){
 //SELECT文を準備
 String sql = "SELECT ID, NAME, AGE FROM, EMPLOYEE";
 PreparedStatement pStmt = conn.prepareStatement(sql);
 //SELECTを実行し、結果表を取得
 ResultSet rs = pStmt.executeWuery();
 //結果表に格納されたレコードの内容を
 //Employeeインスタンスに設定し、ArrayListインスタンスに追加
 while(rs.next(){
 String id = rs.getString("ID");
 String name = rs.getString("NAME");
 int age = rs.getInt("AGE");
 
 Employee employee = new Employee(id, name, age);
 empList.add(employee);
  }
 }catch (SQLException e) {
 e.printStackTrace();
  return null;
   }
 return empList;
  }
 } 
 ```
 # DAOを利用して全従業員情報を検索するクラス
 ```Java
 import java.util.List;
 import model.Employee;
 import dao.EmployeeDAO;
 
 public class SelectEmployeeSample {
   public static void main(String[] args) {
   // employeeテーブルの全レコードを取得
   EmployeeDAO empDAO = new EmployeeDAO();
   List<Employee> empList = empDAO.findALL();
   
   //取得したレコードの内容を出力
   for(Employee emp : empList {
   System.out.println("ID:" +emp.getID());
   System.out.println("名前:"+emp.getName());
   System.out.println("年齢:" +emp.getAge() + "¥n:");
   }
   }
}



