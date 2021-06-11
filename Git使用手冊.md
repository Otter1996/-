# Git使用手冊
###### 剛學習git，對於指令不是很熟悉，希望可以透過撰寫筆記來增加印象

## 初探git
1. 在適合的地方建立一個專案資料夾，ex:project-1，並把所有相關的東西都放進該資料夾。
2. 在該路徑底下初始化使用指令`git init`，意思是在該專案資料夾裡放入一個隱藏檔案的資料夾(.git)並初始化Git Repository。
3. 這時在該資料夾裡新增檔案，這時使用指令`git status`時就會出現該檔案名稱。
4. 這時如果要把改過的程式或新增的程式加入git裡時，這時候就要打`git add (檔案名稱)`。如果改動的檔案很多這時候就可以打`git add .`將所有程式一次加入到git裡。
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

## 如何跟同事合作同一個專案?
1. 下載Github Repository到本機
2. 在第一次下載Github Repository時必須`git clone (遠端空間的網址) (本機資料夾名稱)`
3. 未來必須要不斷的從github雲端下載合併更新專案，這時候就會用到`git pull (遠端空間的分支 ) (遠端空間的分支)`
4. 上班第一件事就是使用git pull 來合併專案

## 如何查看先前commit的版本紀錄
1. 詳細全部資訊`git log` 
2. 簡易版本資訊`git log --oneline`

## 我想查看某次commit到底commit了什麼東西，怎麼做?
1. `git log`查看commit紀錄，並記下commit ID。
2. 使用`git show (commit碼)`就可看到commit的東西。

## Git branch使用
1. git branch的功用是在不想要動到主程式的情況下新增一個功能，這時候就會用到git branch。而分支的目的就是將整體流程做一個分岔的保存。
2. 想查看專案裡有哪些分支或者是某分支是否被創建，可以輸入指令`git branch`。第一次打git branch會出現*master代表主branch
3. 想創建分支需要輸入指令`git branch (分支名)` 
4. 在一個Repository底下，如果要觀看另一個版本，必須要透過移動HEAD來進行，想要進入到某分支裡，就必須使用`git checkout (分支名)`
5. 想要同時創建一個分支，並且將HEAD指向該分支的語法:`git checkout -b (分支名)`
6. 刪除分支:`git branch -d (分支名)`
7. 查看HEAD目前所指向的分支內容:ll
8. 如果想要把自己在本地端創的分支也推上github就必須要該branch裡輸入指令`git push origin (分支名)`
9. 如果想要刪除遠端分支其命令如下`git push origin :(分支名)`
10. 如果想要把本地的branch叫feature1但是遠端的branch不想叫feature1該怎麼做呢?輸入指令`push origin feature:(遠端branch名稱)`

## Git Merge使用
1. 假設我有兩個分支：master和branch，今天我要將branch合併(merge)至master時，請注意必須將目前分支指回master
2. `git checkout master`將HEAD指向master
3. `git merge (分知名稱)`

## gitignore文件介紹
1. gitignore文件可以避免一些不必要上傳的資料或者是一些敏感資料被空開在github上。
2. gitignore文件規則:

| *.sh | .settings/ | !.txt |
| -------- | -------- | -------- |
| 代表所有的.sh檔都會</br>被忽略| 代表setting這個資料夾內</br>所有檔案都是要被忽略的    | 代表所有的txt文件都是</br>不能夠被忽略的| 


| /a/*.class |
| -------- | 
| 代表所有a資料夾內的.class檔都是要被忽略的|

## 分支衝突解決辦法
#### 如果看到程式碼裡生成了以下文字
<<<<<<HEAD<br>
OOOOOXXXXX<br>
==========<br>
OOXXXXXXXX<br>
&ensp;>>>>>>>>>(branch name)<br>
#### 代表merge時發生衝突，原因是因為有人在你pull之後又push到該分支上，而你的程式碼又跟別人重疊，怕你不知道裡面內容而覆蓋過去。上面的內容是本地的分支內容；下面的內容是遠端主機的分支內容。可以手動刪除看欲留下哪裡的內容。

## Git後悔系列
1. 情況一:已commit的版本想回頭加入某些內容，但還是維持在該commit版本的方法?<p></p>
Ans: `git commit --amend --no-edit`，代表不想改發佈內容。雖然不會commit出新版本，但是commit ID還是會改變。

2. 情況二:如果已經git add的檔案想要反悔，回到Modifiy的狀態如何做到?<p></p>
Ans:`git reset (檔案名)`

3. 情況三:如果已經commit的檔案想要反悔，回到Modifiy的狀態如何做到?<p></p>
Ans:`git reset (所在分支EX:master)`

4. 情況四:如果想要回朔版本可以怎做?<p></p>
Ans:<br>
1.`git reset --hard HEAD`//往前回朔一個版本，HEAD表示指針<br>
2.`git reset --hard HEAD^^`//git reset --hard HEAD~2 皆表示往前回朔兩個版本<br>
3.`git reset --hard (版本號碼)`//可以回朔到指定的版本

5. 情況五:如果回朔了以後又反悔了，該怎麼辦?<p></p>
Ans:<br>
1.使用`git reflog`可以看到HEAD(指針)每一步的紀錄<br>
2.看到了指針先前的紀錄之後，就可以使用`git reset --hard (版本ID/HEAD@{數字})`<br>
3.或者是使用checkout來針對**單個文件**回朔所進行的操作
`git checkout (欲回朔到該版本內容的ID) -- (文件名稱EX:1.py)`
4.`git revert`可以撤銷某一次操作，此次操作之前和之後的commit和history都保留，並把這次撤銷為一次最新的提交

## 如何看到修改狀態內容?
1. `git diff`必須使用git add之後才會有效
2. `git diff --cached`可以使用在git add之後

## 如果要複製別人的Repository到自己的Repository或是幫別人的Repository做出貢獻可以怎麼做?
1. `git clone (遠端舊專案網址)`
2. `git remote -v` //查看遠程分支資訊
3. 下載下來的本機資料跟遠端做連結`git remote add (專案名稱EX:upstream//由於不是自己的專案所以名稱不會取作origin) (該更新專案網址//非本地repository)`
4. `git remote -v `這時候會出現一組origin(舊版本) 跟一組upstream(新版本)
5. 這時候就可以使用`git fetch upstream` 把新專案內容抓下來
6. 合併舊專案內容和新專案內容。
7. 如果只是為了同步`git rebase upstream/master`,如果對內容有更動就應改使用`git merge`


## Git小細節
1. `git pull` = `git fetch` + `git merge`
2. `cd..` = 回到資料夾的上一層
3. `cd~`= 回到電腦的最外層，類似根目錄
4. `touch` (檔案名稱.類型) = 新增這個檔案
5. `cd(空白)` = cd加入空白鍵之後，再按下tab會出現當前目錄的清單
6. `clear` = 清除shell的內容
7. `wq!` = 儲存並退出
8. `w` = 存檔
9. `q` = 離開
10. `i` / `a` / `o` =進入Isert模式
11. `esc` / `ctrl+[` = 退回Normal模式