# サーブレットクラスの実行方法

サーブレットクラスを実行するには、ブラウザでサーブレットクラスのURLを指定してリクエストします。 サーブレットクラスのURLは、次の形式で指定します。　　　　＝＝＝＞　http://<サーバ名>/<アプリケーション名>/<URLパターン> サーブレットクラスはURLパターンを設定しないとリクエストして実行することができません。

## URLパターンの設定
アノテーションで付加された情報は、外部ツールに読み込ませることが可能です。
サーブレットクラスに、@WebServletアノテーションを加えると、アプリケーションサーバがそれを読み取り、URLパターン設定を行います。（めっちゃ重要じゃん）
### 書き方
```Java
@WebServlet("/URLパターン")
```
※ javax.servlet.annotation.WebServletをインポートする必要がある。

```Java
import javax.servlet.annotation.WebServlet;


@WebServlet("/hello")
public class HelloServlet extends HttpServlet {


}

```

### 実際にサーブレットクラスを実行してみる
サーブレットクラスにURLパターンを設定したら、ブラウザからリクエストして実行できるようになります。ブラウザからリクエストする方法には、HTMLファイルをリクエストするときと同様、次の２つの方法があります。

- 方法① ブラウザを起動してURLを入力する。（このとき、アプリケーションサーバーを起動しておく必要がある。）
- 方法② Eclipseの実行機能を利用する
- 方法③ サーブレットクラスへのリンクをクリックする

```Java
<a href= "/アプリケーション名/URLパターン">リンク文字列</a>
```


#実際に作ってみよう！

- まずは　プロジェクトを作って右クリックー>サーブレットー> クラス名をHelloServlet(先頭は大文字）
- srcの下に自動的に作られる。
- いろんなものが書かれた状態である。これらは次の三つを満たしている
  - javax.servlet.http.HttpServlet　クラスを継承する。
  - doGet(), doPost()メソッドをオーバーライドして使う
  - サーブレット関係のクラスをインポートする。

## オーバーライドのサンプルを見てみよう！
```Java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
response.setContentType("text/html; charset- UTF-8");
PrintWriter out = response.getWriter();
out.print("<html>");
out.print("<head>");
out.print("<title>Servlet</title>");
out.print("</head>");
out.print("<body><h1>Hello, Servlet</h1></body>");
out.print("</html>");
```

## 変更したとき
サーバーを実行する（一番手っ取り早いのは、サーバーを再起動する)

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

# 【EL式の演習問題】
Exampleプロジェクトに、以下を作成して下さい。
 -elパッケージを作成
    -プロジェクト名（Example）右クリック→新規→その他→ Java > パッケージ
 -ElSampleServlet というサーブレットクラスを作成
    -elパッケージ右クリック→新規→サーブレット→クラス名：ElSampleServlet
 -ElSample.jsp を作成
  -WEB-INF > JSP フォルダに作成すること
 -libにtablibのjarを配置する
 
 ## Check for update




