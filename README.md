# lab4_6

Gửi dữ liệu sang màn hình mới

## Các bước làm và mã nguồn
1. Tạo  một lớp chứa hai phần dữ liệu: tiêu đề và mô tả
```
class Todo {
  final String title;
  final String description;

  Todo(this.title, this.description);
}
```
2. Tạo danh sách các việc cần làm
* Tạo danh sách việc cần làm
```
final todos = List<Todo>.generate(
  20,
  (i) => Todo(
    'Todo $i',
    'A description of what needs to be done for Todo $i',
  ),
);
```
* Hiển thị danh sách các việc cần làm bằng ListView
```
ListView.builder(
  itemCount: todos.length,
  itemBuilder: (context, index) {
    return ListTile(
      title: Text(todos[index].title),
    );
  },
);
```
3. Tạo màn hình Todo để hiển thị danh sách
```
class TodosScreen extends StatelessWidget {
  final List<Todo> todos;

  //requiring the list of todos
  TodosScreen({Key key, @required this.todos}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Todos'),
      ),
      //passing in the ListView.builder
      body: ListView.builder(
        itemCount: todos.length,
        itemBuilder: (context, index) {
          return ListTile(
            title: Text(todos[index].title)
          );
        },
      ),
    );
  }
}
```
4. Tạo màn hình chi tiết để hiển thị thông tin về việc làm
```
class DetailScreen extends StatelessWidget {
  // Declare a field that holds the Todo.
  final Todo todo;

  // In the constructor, require a Todo.
  DetailScreen({Key key, @required this.todo}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // Use the Todo to create the UI.
    return Scaffold(
      appBar: AppBar(
        title: Text(todo.title),
      ),
      body: Padding(
        padding: EdgeInsets.all(16.0),
        child: Text(todo.description),
      ),
    );
  }
}
```
5. Điều hướng và chuyển dữ liệu đến màn hình chi tiết
```
ListView.builder(
  itemCount: todos.length,
  itemBuilder: (context, index) {
    return ListTile(
      title: Text(todos[index].title),
      // When a user taps the ListTile, navigate to the DetailScreen.
      // Notice that you're not only creating a DetailScreen, you're
      // also passing the current todo to it.
      onTap: () {
        Navigator.push(
          context,
          MaterialPageRoute(
            builder: (context) => DetailScreen(todo: todos[index]),
          ),
        );
      },
    );
  },
);
```
