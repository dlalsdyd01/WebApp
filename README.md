
# 간단한 웹 애플리케이션 코드만들기  
이름과 번호, 생년월일을 받아 addbook.txt파일에 csv형식으로 저장하는 어플리케이션



터미널에서 가상환경 만들기  
```conda create -n webApp python=3.9```  


Flask 프레임워크 설치  
```pip install flask```  

# app.py 코드 작성  
```from flask import Flask, render_template, request, redirect
import csv

app = Flask(__name__)

# Route for the home page
@app.route('/')
def index():
    return render_template('index.html')

# Route to handle form submission
@app.route('/add', methods=['POST'])
def add_contact():
    name = request.form['name']
    phone = request.form['phone']

    # Save to addbook.txt in CSV format
    with open('addbook.txt', 'a', newline='', encoding='utf-8') as file:
        writer = csv.writer(file)
        writer.writerow([name, phone])

    return redirect('/')

if __name__ == '__main__':
    app.run(debug=True)
```


# index.html 코드작성
 
  
```<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Address Book</title>
</head>
<body>
    <h1>Address Book</h1>
    <form action="/add" method="post">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
        <br><br>
        <label for="phone">Phone:</label>
        <input type="text" id="phone" name="phone" required>
        <br><br>
        <button type="submit">Add Contact</button>
    </form>
</body>
</html>
```

# style.css 코드 작성  
```body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f9;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
}

/* 헤더 스타일 */
header {
  width: 100%;
  background-color: #4CAF50;
  color: white;
  padding: 10px 0;
  text-align: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

header h1 {
  margin: 0;
  font-size: 24px;
}

/* 메인 컨텐츠 스타일 */
main {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

/* 폼 컨테이너 스타일 */
form {
  background-color: #ffffff;
  padding: 20px 30px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 400px;
}

/* 라벨 스타일 */
label {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
  color: #555555;
}

/* 입력 필드 스타일 */
input[type="text"],
input[type="date"] {
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  border: 1px solid #cccccc;
  border-radius: 5px;
  box-sizing: border-box;
  font-size: 14px;
}

/* 입력 필드 포커스 효과 */
input[type="text"]:focus,
input[type="date"]:focus {
  border-color: #4CAF50;
  outline: none;
  box-shadow: 0 0 5px rgba(76, 175, 80, 0.5);
}

/* 버튼 스타일 */
button {
  width: 100%;
  padding: 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #45a049;
}

/* 반응형 디자인 */
@media (max-width: 500px) {
  form {
      padding: 15px;
  }

  header h1 {
      font-size: 20px;
  }

  button {
      font-size: 14px;
  }
} 
```


# 프로그램 실행 방법  
python app.py  
브라우저에서 http://127.0.0.1:5000 로 접속하여 이름과 전화번호 저장가능한 FLASK애플리케이션 완성  

![image](https://github.com/user-attachments/assets/57f3306c-931b-41a9-ae39-74e437758986)  




# 코드 설명  
1. index.html
   

```<body>
    <h1>Address Book</h1>
    <form action="/add" method="post">
        <label for="name" class="label-name">Name:</label>
        <input type="text" id="name" name="pyname" required>
        <br><br>
        <label for="phone">Phone:</label>
        <input type="text" id="phone" name="pyphone" required>
        <br><br>
        <button type="submit">Add Contact</button>
    </form>
</body>
```
위 코드에서 form action="/add"는 현재 url에서 /add 라우터를 호출한다.  
라우터가 호출되면 py 파일에서 해당 라우터 함수가 실행 된다.  
input type="text" id="name" name="pyname" required 에서 id=name은 html 또는 js에서 사용되는 이름이고  
pyname, pyphone은 py 파일에서 POST로 데이터를 받을때 사용되는 이름이다.  

2. app.py
   
```
@app.route('/')
def index():
    return render_template('index.html')

# Route to handle form submission
@app.route('/add', methods=['POST'])
def add_contact():
    name = request.form['pyname']
    phone = request.form['pyphone']

    # Save to addbook.txt in CSV format
    with open('addbook.txt', 'a', newline='', encoding='utf-8') as file:
        writer = csv.writer(file)
        writer.writerow([name, phone])

    return redirect('/')
```
@app.route('/')는 해당 웹페이지 주소 localhost/를 호출 할때 실행되는 라우트이고
def index(): 는 이때 실행 되는 함수이다.
return render_template('index.html') 이것은 index.html을 웹 브라우저에 랜더링 하라는 것.

이후에 index.html에서 action으로 지정된 "/add"가 호출되면
@app.route('/add', methods=['POST'])가 호출된다. 이것은 localhost/add 를 한것과 같다.
def add_contact(): 함수가 실행 된다. 이후 코드는 기존의 파이썬 코드와 동일 하다.
