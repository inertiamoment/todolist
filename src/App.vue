<template>
  <div class="container d-flex flex-column align-items-center justify-content-center">
    <!-- ロゴ画像の追加 -->
    <img src="@/assets/logo.jpg" alt="Logo" class="my-4" style="max-width: 200px;" />
    
    <!-- ToDo追加フォーム -->
    <div class="search-bar mb-3">
      <input 
        type="text" 
        class="search-input" 
        v-model="newTodoText" 
        placeholder="新しいToDoを入力" 
      />
      <button class="flat-btn add-btn" @click="addTodo">追加</button>
    </div>

    <!-- ToDoリスト -->
    <p v-if="todos.length === 0" class="alert alert-info text-center">ToDoがまだありません！</p>
    <ul class="list-group text-center w-100">
      <li v-for="todo in todos" :key="todo.text" class="list-group-item position-relative d-flex align-items-center" @click="toggleDeleteButton(todo)">
        <div class="d-flex align-items-center w-100">
          <span :class="{ 'todo-done': todo.isDone }">{{ todo.text }}</span>        <button v-if="todo.showDelete" class="delete-btn position-absolute end-0" @click.stop="removeTodo(todo)">削除</button>
        </div>

      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodoText: '',
      todos: [],
    };
  },
  methods: {
    addTodo() {
      if (!this.newTodoText) return alert('文字を入力してください');
      this.todos.push({
        isDone: false,
        text: this.newTodoText,
        showDelete: false, // 削除ボタンの表示状態を追加
      });
      this.newTodoText = '';
    },
    toggleDeleteButton(todo) {
      todo.showDelete = !todo.showDelete; // タスクをクリックしたときに削除ボタンをトグル
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo);
    },
  },
};
</script>

<style>
/* グローバルスタイル */
body {
  background-color: #EEEEEE; /* ライトグレー */
  margin: 0; /* デフォルトのマージンを削除 */
  height: 100vh; /* 画面の高さを100%に設定 */
  display: flex; /* フレックスボックスを使用 */
  justify-content: center; /* 水平方向の中央配置 */
  align-items: center; /* 垂直方向の中央配置 */
}

/* コンテナを画面中央に配置 */
.container {
  width: 600px; /* 幅を600pxに設定 */
  text-align: center; /* テキストを中央に配置 */
}

/* ToDoが完了した場合のスタイル */
.todo-done {
  text-decoration: line-through;
  color: #00ADB5; /* アクアブルー */
}

/* サーチバー風入力フォーム */
.search-bar {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}

.search-input {
  width: 70%; /* 入力フィールドの幅を70%に設定 */
  padding: 10px;
  border: 1px solid #222831;
  border-radius: 50px; /* 楕円形にする */
  background-color: #fff;
  outline: none;
  box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.2); /* 影をつけて立体感を出す */
  transition: all 0.3s ease;
  font-size: 16px;
  color: #222831;
}

.search-input:focus {
  border-color: #00ADB5;
  box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.3); /* フォーカス時に影を強調 */
}

.flat-btn {
  border: none;
  padding: 10px 20px;
  border-radius: 50px; /* ボタンも楕円形にする */
  background-color: #00ADB5;
  color: #EEEEEE;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-left: 10px;
}

.flat-btn:hover {
  background-color: #393E46;
}

.add-btn {
  background-color: #00ADB5;
}

.delete-btn {
  background-color: #FF6B6B; /* 削除ボタンの色 */
  border-radius: 50px; /* ボタンを楕円形に */
  margin-left: 10px; /* ボタンの左マージン */
}

.delete-btn:hover {
  background-color: #FF4D4D; /* 削除ボタンのホバー色 */
}

/* リストアイテムのスタイル */
.list-group-item {
  background-color: #00ADB5; /* バナー風の背景色 */
  color: #FFFFFF; /* テキスト色を白に設定 */
  border-color: #00ADB5; /* 境界線の色 */
  border-radius: 30px; /* 楕円形にする */
  padding: 10px 20px; /* パディングを追加 */
  margin-bottom: 10px; /* アイテム間のスペース */
  position: relative; /* ボタンを絶対配置するために相対位置を設定 */
  cursor: pointer; /* カーソルをポインタに */
}

/* スペーシングの追加 */
.ms-auto {
  margin-left: auto; /* ボタンを右に寄せる */
}
</style>