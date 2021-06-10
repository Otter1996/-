# Git使用手冊
###### 剛學習git，對於指令不是很熟悉，希望可以透過撰寫筆記來增加印象

## 初探git
1. 在適合的地方建立一個專案資料夾，ex:project-1，並把所有相關的東西都放進該資料夾。
2. 在該路徑底下初始化使用指令`git init`，意思是在該專案資料夾裡放入一個隱藏檔案的資料夾(.git)。
3. 這時在該資料夾裡新增檔案，這時使用指令`git status`時就會出現該檔案名稱。
4. 這時如果要把改過的程式或新增的程式加入git裡時，這時候就要打`git add\(檔案名稱)`。如果改動的檔案很多這時候就可以打`git add .`將所有程式一次加入到git裡。
5. 重新`git status`會發現檔名已呈現綠色(表示已經加入追蹤)。
6. 使用git commit -m"(本次commit的備註)"，用來新增一個版本。
7. 使用git push將檔案推到Github的Repository上(可以翻作雲端的專案空間)。

## 初探Github
1. github最主要的運作單位就是repository(可以翻作雲端的專案空間)
2. Repository name可以隨便填。
3. 如果你想要把你的專案分享給同事，可以利用github，將專案紀錄上傳到github的雲端空間。
4. 就算獨立開發，也可以傳到github備份。

## Git與Github的連結
1. 本機端專案跟Github連接，`git remote add (origin/我們替遠端命名的名稱) + 雲端專案空間的連線網址`。
2. `git remote -v`查詢關聯的Repository，-v會顯示得更詳細。如果顯示空白代表目前沒有關聯的雲端空間。
3. `origin URL (fetch)`代表抓取的網址。
4. `origin URL (push)`代表上傳的網址。
5. `git push (遠端空間的名稱 ex:origin) (遠端空間的分支ex:master)`。用途為，將修改或新增的檔案上傳到Github雲端專案空間

## h2