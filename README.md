這是一個使用 Vue 3 製作的便利貼應用：
新增/刪除代辦事項
編輯事項內容與日期
自動儲存至瀏覽器（localStorage）
新增多張便利貼（不同顏色）
使用技術：
Vue 3 + <script setup>
Composition API
LocalStorage 持久化資料
基本 HTML/CSS 排版
專案結構：
src/
├── components/
│   └── todoApp.vue        # 單張便利貼元件
├── App.vue                # 外層容器，可新增多張便利貼
└── main.js                # Vue 應用啟動點
