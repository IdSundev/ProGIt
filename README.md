# Python for Data Analysis, 2nd Edition

Repositori ini berisi catatan dari ebook ProGit, 2nd Edition by Scott Chacon and Ben Straub.
https://git-scm.com/book/en/v2

catatan: sebelum merging ke local master biasakan pull dulu master nya supaya local master sama dengan remote master.

GIT BASIC
=========
Setting Identitas
```
$ git config --global user.name "Cef Syarif"
$ git contig --global user.email chefdeveloper29@gmail.com 
Setting Identitas di local repository, --local ini berfungsi untuk mengenali account mana yang dipakai untuk memanage repository di local
$ git config --local user.name "cefsyarif294"
$ git config --local user.email cef.syarif@gmail.com
$ git config --list
$ git config user.name
$ git config user.email
```

Status di git
1. UNtracked
2. Unmodified
3. Modified
4. Staged

Check status File
```
$ git status
```

Tracked File
```
$git add nama_file
```

Ignoring Files
file yg di ignore bahkan tidak dikenali git sebagai untracked.
- buat file .gitignore
isinya menggunakan regex, contoh:
*.[0a] => mengignore smeua file berekstensi *.a atau *.b
- Contoh penggunaan .gitignore:
# ignore all .a files
*.a
# but do track lib.a, though you're ignoring .a files above
!lib.a
# only ignore the TODO file in the current directory, not subdir/TODO
/TODO
# ignore all files in the build/ directory
build/
# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt
# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf
Github menyediakan file-file gitignore untuk project menggunakan teknologi tertentu: 
https://github.com/github/gitignore

Sekilas Fungsi git diff
Jika kita memodifikasi sebuah file (not staged), maka kita bisa menggunakan git difff untuk melihat apa yang terjadi pada file tersebut (bagian apa yang ditambahkan, dan bagian apa yang dikurangi?)
```
$ git diff --staged
```
perintah diatas untuk melihat apa yang ditambahkan ke file yang status nya staged.

Commiting Your Changes 
```
$ git commit -m "Story 182: Fix benchmarks for speed"
```

Skipping the Staging Area
maksudnya adalah ketika kita memodifikasi sebuah/ beberapa file dan belum melakukan staging file dengan cara git add nama_file tapi kita ingin mengcommit nya langsung maka perintahnya adalah:
```
$ git commit -am "Message of Commit"
```

VIEWING COMMIT HOSTORY
- Menampilkan 2 log commit teratas
```
git log -2
```
- Menampilkan 2 log commit teratas dengan detail nya
```
git log -p -1
```
- Menampilkan log commit dengan tambahan informasi singkat file apa saja yang mengalami perubahan
```
git log --stat
```
- Menampilkan log commit hanya id dan keterangan nya saja
```
git log --pretty=oneline
```
- MENAMPILKAN LOG COMMIT DENGAN FORMAT TERTENTU
```
git log --pretty=format:"%h, %cn %ce %cd: %s"
git log --pretty=format:"%h, %cn %ce %cr: %s"
```
- Menampilkan log commit dengan history branch dan merge
```
git log --pretty=format:"%h, %s" --graph
```
- Menampilkan log commit dari kapan sampai kapan dan oleh siapa
```
git log --pretty=format:"%h %cd - %s" --author="Cef Syarif" --since="2020-01-01" --before="2020-03-01"
```
- Membuat perintah alias di cmd untuk menampilkan log commit dalam bentuk graph
```
alias graph="git log --all --decorate --oneline --graph"
```


UNDOING THINGS
- Pentingnya fungsi git commit --amend
Misalkan kita sedang melakukan koding untuk menambahkan fitur CRUD data Bencana kemudian kita lakukan commit ke repositori dengan message "Menambahkan fitur CRUD data Bencana". Nah karena keteledoran kita ada 1 field yang tidak memiliki inputan, akhirnya kita tambahkan 1 field tersebut di kodingan kita. Nah supaya codingan baru tersebut tidak disimpan di commit yang baru, kita bisa menyimpan kodingan baru tersebut di commit yang sudah ada ("Meambahkan fitur CRUD data Bencana") dengan perintah:
```
git commit --amend
```
Selain itu perintah diatas juga bisa digunakan untuk merubah pesan commit kita.
- Merubah status staged ke unstaged
```
git reset HEAD nama_file yang mau di unstaged
```
- Merubah file dengan status modified ke status semula (Fungsi git checkout -- nama_file)
Misal, kita memodifikasi kode tertentu kemudian kita tidak jadi memodifikasi kode tersebut, artinya kita ingin file kita kembali ke kondisi sebelum statusnya modified. Maka gunakan perintah
```
git checkout -- nama_file
```

MANAJEMEN REMOTE REPOSITORY
- Clone
```
git clone link
```
- Melihat remote repository
```
git remote -v
```
- Menambah remote repository baru
```
git remote add <shortname>(nama untuk kita mengakses repository remote nya) [url]
```
contoh: 
```
git remote add pb https://github.com/paulboone/ticgit
```
- Perbedaan git pull dan git fetch: https://www.petanikode.com/git-pull-fetch/
git pull digunakan ketika kita menarik data dari remote repository ke local repository sebelum ada commit apapun, sedangkan git fetch digunakan ketika kita menarik data dari remote repository ke repository local yang sudah ada commit sebelumnya, link diatas caranya.
git fetch digunakan untuk melihat perubahan yang ada di remote repository

- Melihat ke repo mana kita mengambil data, dan ke repo mana kita push data bisa menggunakan perintah:
```
git remote show origin
```
- Untuk melihat remote repositori apa saja yang ada bisa menggunakan perintah:
```
git remote
```
- Cara merename remote repository
```
git remote rename pb<nama_lama> paul<nama_baru>
```
- Menghapus remote repository
```
git remote remove paul
```

TAGGING
- Karena tidak terlalu penting sejauh ini, jadi baca aja di ebook nya

GIT BRANCHING
=============
- default branch name in git is master
- HEAD adalah pointer yang menunjukan branch yang sedang aktif. In Git, this is a pointer to the local branch you’re currently on.
- Cara melihat di branch mana pointer berada:
```
git log --oneline --decorate
```
- Perintah git log yang proporsional untuk tracking, branching, dll
```
git log --oneline --decorate --graph --all
```
- Cara melihat daftar branch yang ada di git
```
git branch / git branch -a
```
- Cara berpindah branch:
```
git checkout nama_branch
```
- Basic Branching and Merging
Secara sederhana konsepnya adalah sebagai berikut: misalkan kita punya sebuah production code, production code ini terletak di branch master. Nah suatu ketika ada penambahan fitur baru atau ada sebuah bug, maka kita tidak melakukan pekerjaan tersebut di branch master, tapi kita melakukan pekerjaan tersebut di branch baru yang kita buat. Setelah kode yang kita buat dari branch baru tersebut di test atau diuji dan lolos maka langkah selanjutnya adalah kita melakukan merging dari branch dimana kita bekerja ke branch master, setelah kode kita ada di production alias branch master maka langkah selanjutnya adalah menghapus branch yang sudah kita buat tadi.
- Membuat branch sekaligus berpindah ke branch tersebut
```
git checkout -b nama_branch_baru, perintah ini sama dengan
git branch nama_branch_baru
git checkout nama_branch_baru
```
- Intinya basic branching itu adalah apa yang selama ini udah dilakukan, maka untuk contoh bisa dilihat di ebook 'Basic Branching', 'Basic Merging', 'Basic Merge Conflict'
Branch Management
- list all branch:
```
git branch
```
- list last commit setiap branch:
```
git branch -v
```
- Melihat branch mana saja yang pernah di merge ke branch yang sekarang sedang aktif:
```
git branch --merged
```
- Melihat branch mana saja yang ada tapi tidak pernah di merged ke branch yang sekarang sedang aktif:
```
git branch --no-merged
```
- Kita bisa menggunakan --merged/--no-merged pada branch yang sedang tidak aktif dengan cara:
```
git branch --merged/--no-merged nama_branch
```

Branching Workflows
Branching Workflows ada dua, ada Long-Running Branches ada juga Topic Branches
- Long-Running Branches
Long-Running Branches adalah kondisi dalam development cycle yang sederhana dimana production code ada di branch master, dan ketika kita mau mendevelop fiture tertentu kita bikin branch baru, kemudian ketika fitur yang dibuat memiliki sub topic maka fokus pada sub topic tersebut, ketika sub topic tersebut beres maka sub topic akan di merge ke branch fiture, dan setelah branch fiture beres maka branch fiture tersebut akan di merge ke branch master.
- Topic Branches
Topic Branches ini paling recomended, jadi setiap branch mewakili topic2 tertentu, ada topic yang menambah fiture baru ada topic yang berfungsi untuk mengatasi bug tertentu, ada juga topic branch utama atau branch master. Contohnya bisa dilihat di ebook.

Remote Branches
- jika menggunakan git clone -o booyah maka remote branch nya tidak lagi origin/master tapi booyah/master
- Melihat pointer yang ada di remote repository
```
git remote show nama_branch<origin>
```
atau
```
git ls-remote nama_branch<origin>
```

PENTING: Perbedaan git pull dengan git fetch
kapan sih waktu yang tepat menggunakan git pull dan git fetch?
- Perintah git pull akan mengambil commit terbaru lalu otomatis menggabungkan (merge) dengan branch yang aktif.
- Sedangkan git fetch akan mengambil commit saja. Perintah git fetch tidak akan langsung melakukan merge.
- Apabila kita sudah melakukan commit di repository lokal, maka yang kita gunakan adalah git fetch.
- Sedangkan apabila kita tidak pernah melakukan apa-apa di lokal repository, kita bisa menggunakan git pull.

REBASING
- Disini ada contoh penggunaan git rebase --continue ketika terjadi conflict: https://thesolidsnake.wordpress.com/2014/10/03/belajar-memakai-git-rebase/
- Dasar Rebase bisa dilihat di web programming unpas
-  Menggabungkan 9 commit terakhir menjadi sebuah commit:
```
git rebase -i HEAD~10
```

GIT ON THE SERVER
=================

Distributed Workflow
====================
- Centeralized worklow adalah cara kerja pada git atau cara bekerja menggunakan git dimana pada workflow ini cara kerja nya mirip subversion, jadi ada sebuah repository tempat beberapa developer berkolaborasi, dimana branch origin/master adalah sentralnya misalkan ada 2 orang developer sedang membangun situs yang sama maka developer pertama akan melakukan push codenya ke origin/master, nah ketika developer kedua akan push codenya ke origin/master developer ke dua harus melakukan merge terlebih dahulu dari origin/master ke local master (melakukan pulling).
Simply set up a single repository, and give everyone
on your team push access; Git won’t let users overwrite each other. Say John and Jessica both start
working at the same time. John finishes his change and pushes it to the server. Then Jessica tries to
push her changes, but the server rejects them. She is told that she’s trying to push non-fast-forward
changes and that she won’t be able to do so until she fetches and merges. This workflow is
attractive to a lot of people because it’s a paradigm that many are familiar and comfortable with.
This is also not limited to small teams. With Git’s branching model, it’s possible for hundreds of
developers to successfully work on a single project through dozens of branches simultaneously.
- Integration-Manager Workflow adalah cara kerja yang biasa kita gunakan ketika kita menjadi contributor dalam sebuah proect di github, contoh controbutor laravel.
To contribute to that project, you create your own public clone of the project and push your changes to
it. Then, you can send a request to the maintainer of the main project to pull in your changes. The
maintainer can then add your repository as a remote, test your changes locally, merge them into
their branch, and push back to their repository
1. The project maintainer pushes to their public repository.
2. A contributor clones that repository and makes changes.
3. The contributor pushes to their own public copy.
4. The contributor sends the maintainer an email asking them to pull changes.
5. The maintainer adds the contributor’s repository as a remote and merges locally.
6. The maintainer pushes merged changes to the main repository.
This is a very common workflow with hub-based tools like GitHub or GitLab, where it’s easy to fork
a project and push your changes into your fork for everyone to see. One of the main advantages of
this approach is that you can continue to work, and the maintainer of the main repository can pull
in your changes at any time. Contributors don’t have to wait for the project to incorporate their
changes — each party can work at their own pace.
- Dictator and Lieutenants Workflow
baca di ebook aja soalnya case nya jarang.

Contributing to a Project
Karena git sangat flexible, maka cara untuk berkonstribusi kedalam projek itu berbeda-beda. 
Ada beberapa variabel yang menadi pertimbangan:
1. Active contributor count
2. Chosen workflow
3. Commit access
4. External contribution method.
All these questions can affect how you contribute effectively to a project and what workflows are
preferred or available to you. We’ll cover aspects of each of these in a series of use cases, moving
from simple to more complex; you should be able to construct the specific workflows you need in
practice from these examples
- Commit Guideline
pastikan sebelum commit tidak ada error atau whitespace untuk memeriksanya gunakan git diff
pastikan melakukan commit per judul, maksudnya ketika kita membuat fitur commit nya jangan distukan dengan ketika kita melakukan debuging.
This approach also makes it easier to pull out or revert one of the changesets if you need to later.
commit yang dibuat harus menjelaskan history dari apa yang dilakukan
- Contributing to a proect
1. Private small team => ini yang selama ini ada didalam benak aku jadi beberapa developer bekerja sama dengan menjadikan branch master sebagain induknya, dan ketika ada penambahan fitur atau debuging maka dibuat di branch terpisah kemudian setelah di review dan ok baru di merge ke master
2. Private managed team => 

Contribusi di GIthub
- Lakukan Fork, langkah pertama yang harus dilakukan ketika kita akan berkontribusi pada repository public adalah melakukan fork terhadap project

Keeping upstream ini tips supaya kita bisa melakukan pull request secara cleanly



PERINTAH-PERINTAH YANG ADA DI GIT
=================================
```
$ git config --global user.name "Cef Syarif"
$ git config --global user.email chefdeveloper29@gmail.com
```
KETERANGAN: Menambahkan konfigurasi secara global account mana yang sedang aktif

```
$ git config --local user.name "Cef Syarif"
$ git config --local user.email cef.syarif@gmail.com
```
KETERANGAN: Jika kita punya beberapa account github/ semisalnya, dan untuk repo tertentu kita menggunakan account tertentu supaya dikenali (autentikasi), maka setting diatas bisa digunakan. 

```
$ git config --global core.editor "code --wait"
$ git config --global core.editor "'C:/Program Files/path untuk vscode nya' -multiInst -nosession"
```
KETERANGAN: Menjadikan visual studio code sebagai default code editor

```
$ git config --list
```
KETERANGAN: Melihat konfigurasi yang sudah dilakukan

```
$ git config user.name
```
KETERANGAN: Mengakses nama pengguna

```
$ git init
```
KETERANGAN: Menginisialisasi sebuah repositori lokal

```
$ git clone <url>
$ git clone  https://github.com/libgit2/libgit2
```
KETERANGAN: Melakukan cloning repositori ke local kita

```
$ git clone  https://github.com/libgit2/libgit2 mylibgit
```
KETERANGAN: Melakukan cloning repository server ke local dan merubah nama foldernya dari libgit2 ke mylibgit

```
$ git status
```
KETERANGAN: Memeriksa status dari file-file yang ada (untracked, modified, stagged)

```
$ git add <nama_file>
```
KETERANGAN: Tracking New Files

```
$ git add <nama_file>
```
KETERANGAN: Memasukan sebuah file ke kondisi staged

```
$ git add .
```
KETERANGAN: Memasukan semua file yang untracked atau modified ke staged area.

```
$ git diff
```
KETERANGAN: Untuk melihat perubahan apa yang terjadi pada sebuah file.

```
$ git diff --staged
```
KETERANGAN: UNtuk melihat perubahan apa yang terjadi pada sebuah file dalam kondisi stagged.

```
$ git commit -m "Isi pesan dalam commit"
```
KETERANGAN: Melakukan commit

```
$ git commit -am "Isi pesan dalam commit"
```
KETERANGAN: Melakukan commit pada file yang statusnya modified supaya tidak usah melakukan perintah git add <nama_file>

```
$ git log
```
KETERANGAN: Melihat history commit

```
$ git log -2
```
KETERANGAN: Melihat 2 history commit terakhir

```
$ git log --stat
```
KETERANGAN: Melihat history commit + melihat file2 apa yang mengalami perubahan dalam setiap commit

```
$ git log --pretty=oneline
```
KETERANGAN: Melihat history commit hanya id_hash dan message nya saja

```
$ git log --pretty=format:"%h, %cn %ce %cd: %s"
```
KETERANGAN: Melihat history commit dengan format: id_hash nama email date: pesan

```
$ git log --pretty=format:"%h, %cn %ce %cr: %s"
```
KETERANGAN: Melihat history commit dengan format: id_hash nama email waktu: pesan

```
$ git log --all --decorate --oneline --graph
```
KETERANGAN: Melihat history commit beserta history branching dan mergingnya
NOTES: gunakan alias untuk memudahkan aksesnya
```
$ alias graph="git log --all --decorate --oneline --graph"
$ graph
```
KETERANGAN: Hasilnya sama seperti diatas

```
$ git log --since=2.weeks
```
KETERANGAN: Melihat history commit 2 Minggu terakhir

```
$ git log --pretty=format:"%h %cd - %s" --author="Cef Syarif" --since="2020-01-01" --before="2020-03-01"
```
KETERANGAN: Melihat history commit dari author Cef Syarif dari 2020-01-01 sampai 2020-03-01

```
$ git commit -m "Pesan Commit"
$ git add file_yang_kelupaan
$ git commit --amend
```
- VSCODE terbuka
- Edit pesan commit nya jika diperlukan
- Save
KETERANGAN: Jika kita melakukan commit tapi ternyata kita lupa mengedit sebuah file maka kita bisa memasukan file yang kelupaan tersebut kedalam commit dengan perintah amend. Jadi file kelupaan tersebut akan masuk ke commit terkahir.

```
$ git add CONTRIBUTING.md
$ git reset HEAD CONTRIBUTING.md
```
KETERANGAN: Mengembalikan file CONTRIBUTING.md dari status staged ke modified

- Melakukan edit pada file CONTRIBUTING.md
- status file CONTRIBUTING.md jadi modified
```
$ git checkout -- CONTRIBUTING.md
```
KETERANGAN: Unmodifying a Modified File

```
$ git remote -v
```
KETERANGAN: Melihat daftar remote repositori kita

```
$ git remote
```
KETERANGAN: Sama dengan $ git remote -v

```
$ git remote add <nama_remote> <url_repo_remote>
```
KETERANGAN: Menambahkan remote repository ke repo kita dengan nama tertentu

```
$ git fetch <remote>
contoh
$ git fetch origin
$ git status
$ git log --all --decorate --oneline --graph
```
KETERANGAN: Melihat perubahan yang ada di repository remote bernama origin

```
$ git push origin master
```
KETERANGAN: Push penambahan kode kita ke remote repository origin ke brand master nya

```
$ git push -u origin master
```
KETERANGAN: -u adalah parameter yang digunakan untuk men-set upstream, dimana nantinya kita tinggal mengetik perintah git push saja maka code kita akan dikirim langsung ke origin/master

```
$ git remote rename pb paul
```
KETERANGAN: Merubah nama remote repositori dari pb ke paul

```
$ git tag
```
KETERANGAN: Melihat daftar tag yang ada

```
$ git tag -l "v1.8.5*"
```
KETERANGAN: Melihat daftar tag versi ke v1.8.5*
Contoh Output:
v1.8.5
v1.8.5-rc0
v1.8.5-rc1
v1.8.5-rc2
v1.8.5-rc3
v1.8.5.1
v1.8.5.2
v1.8.5.3
v1.8.5.4
v1.8.5.5

```
$ git tag -a v1.4 -m "my version 1.4"
```
KETERANGAN: Membuat tag versi ke v1.4 dengan pesan tag nya "my version 1.4"

```
$ git show v1.4
```
KETERANGAN: Melihat detail history commit dari tag versi ke v1.4

```
$ git push origin v1.5
```
KETERANGAN: push tag ke remote repository yang kita buat

```
$ git push origin --tags
```
KETERANGAN: Push semua tag ke remote repository, jika tag yang kita punya banyak

```
$ git checkout v1.4 #tidak disarankan karena ketika kita mau kembali ke versi terakhir kita harus checkout ke id_hash commit terakhir, jadi gunakan branch baru
```
KETERANGAN: Checkout ke versi/ keadaan dimana tag v1.4 di pointing

```
$ git checkout -b version1.4 v1.4
```
KETERANGAN: Membuat branch baru dimana isi dari branch baru tersebut adalah hasil chekcout ke tag v1.4 dan langsung checkout ke branch baru tsb

```
$ git branch <nama_branch>
```
KETERANGAN: Membuat branch baru

```
$ git checkout <nama_branch>
```
KETERANGAN: Berpindah branch

```
$ git checkout -b <nama_branch>
```
KETERANGAN: Membuat brand baru sekaligus checkout ke branch tsb

```
$ git checkout master
$ git merge hotfix
```
KETERANGAN: Melakukan merging dari branch hotfix ke branch master

```
$ git branch -d hotfix
```
KETERANGAN: Menghapus branch hotfix

```
$ git merge <nama_branch>
```
- Terjadi konflik saat merging
```
$ git status => melihat file2 mana saja yang bentrok
```
- Melakukan perbaikan pada file-file yang conflik
```
$ git add .
$ git commit -m "Pesan Commit"
```
KETERANGAN: Basic Merge Conflicts

```
$ git branch -v
```
KETERANGAN: Melihat semua commit terakhir dari setiap branch

```
$ git push origin serverfix
```
KETERANGAN: Melakukan push branch serverfix ke repo server sehingga nanti di repo server ada branch serverfix tersebut.

```
$ git push origin serverfix:serverfix
```
KETERANGAN: Sama seperti di atas

```
$ git push origin serverfix:awesomebranch
```
KETERANGAN: Sama seperti diatas tapi nanti di remote server nya nama branchnya bukan serverfix tapi awesomebranch

* Nah ketika collabor kita melakukan perintah git fetch origin, maka di origin remote server yang ada di local mereka akan ada remote baru yaitu origin/serverfix, nah untuk mengakses branch tersebut maka collaborator harus memembuat branch baru yang digunakan untuk berkolaborasi membuat/ menyelesaikan serverfix tersebut dengan perintah:
```
$ git checkout -b serverfix origin/serverfix

$ git push origin --delete serverfix
```
KETERANGAN: Menghapus remote branch serverfix di repo server

```
$ git remote add <nama_remote> <url>
```
KETERANGAN: Menambah remote repository ke repo local kita dan mengaksesnya menggunakan <nama_remote> yang telah ditentukan

* Ketika perubahan kita direject oleh remote server boleh jadi ada perubahan di server yang harus kita pull terlebih dahulu, caranya:
```
$ git fetch => Untuk menarik perubahan
$ git status => Untuk melihat perubahan
$ graph
$ git pull
- Terjadi konlik
- Betulkan file-file yang konflik
$ git add .
$ git commit -m "Pesan"
$ git push
$ graph

$ git merge shandikagalih/master
$ git push -u origin master
$ graph
```
KETERANGAN: Melakukan merging dari branch di local repo kita ke remote server dengan nama remote shandikagalih dan branch nya master. Hal ini dilakukan supaya remote local kita up todate dengan remote server pusat, dalam hal ini adalah remote yang kita forking.

BRANCHING WORKFLOWS
===================
1. Long-Running Branches
Jadi didalam workflow ini ada 1 branch master, dibawah branch master terdapat 1 branch develop, dan dibawah branch develop ada branch-branch topic. Ketika proses development semua developer mengerjakan topik tertentu bisa penambahan fitur atau fixing error terhadap fitur tertentu kemudian jika fitur/error tersebut sudah selesai maka branch dari topic tersebut akan di merge ke branch develop untuk di review dan di uji jika dirasa sudah stabil maka branch develop akan di merge ke branch master. Setiap developer dilarang untuk melakukan merge langsung ke master, ini dilakukan untuk menjaga stabilitas code.
2. Topic Branch
Workflow ini adalah workflow yang direkomendasikan karena bisa berguna disemua sekala project. Jadi dalam workflow ini ada 1 buah branch master dimana branch master ini berisi code yang sudah stabil, dan dalam workflow ini para developer akan diberi tugas untuk membuat fitur atau menangani error tertentu dan mengerjakan nya pada branch masing-masing, jika di Long-Running Branches semua developer bekerja pada branch yang sama tapi pada workflow ini developer akan dibagi tugas untuk mengerjakan fitur-fitur tersebut pada branch masing-masing, setelah fitur tersebut selesai maka sebelum melakukan merging ke master repo server, developer harus membuat code di branch fitur uptodate dulu dengan code di branch master yang ada di repo server dengan menggunakan git pull / git fetch baru setelah itu branch nya yang di kirim ke repo server untuk di review bersama setelah dirasa ok baru branch berisi fitur baru tersebut (branch fitur sudah di server) di merge ke master di repo server dan branch baru tersebut di hapus di repo server dan di repo local, baru setelah itu repo local harus di buat uptudate dengan repo server dengan cara dari branch master melakukan pull ke master repo server.

REMOTE BRANCHES
===============
```
$ git fetch origin
```
KETERANGAN: Jika ada yang melakukan push commit ke origin/master di repo server, maka origin/master di repo local kita akan tidak up to date untuk menarik commit baru tersebut supaya origin/master kita sama dengan origin/master repo server maka kita lakukan perinta git fetch origin

* Untuk demo multiple remote server bisa dilihat di ebook progit halaman 83

DISTRIBUTED WORKFLOWS
=====================

DISTIBUTED WORKFLOWS
--------------------
1. Centralized Workflow
Cara kerjanya adalah sebagai berikut, jadi pertama kita buat repository dulu di server bisa github, gilab, atau bitbucket. Kemudian masing-masing developer yang akan berkolaborasi meng clone repository tersebut. Ketika sorang developer akan melakukan push code nya ke remote server dia harus melakukan fetch dan merge terlebih dahulu hal ini dilakukan untuk menghindari reject dari remote server karena sebelumnya ada developer lain yang melakukan push ke remote server.
- Clone Repo
- Create Commit
- Fetch data from server 
- Merging branch master local ke origin/master
- Jika ada konflik maka selesaikan terlebih dahulu
- Push perubahan code kita.
Di dalam workflow ini tidak ada yang namanya integrator jadi semua mempunyai hak akses yang sama. Jadi mungkin SOP yang bisa diterapkan adalah:
a. Buat repository di Git on The Server (Github, Gitlab, Bitbucket)
b. Didalam Remote Server harus ada dua branch: 1. Branch Master => Untuk Release Code / Berisi Code-code yang stabil, 2. Branch Development => Berisi Code-code untuk mereview topic branch yang dikirimkan oleh Developer sampai code-code yang ada di Development ini layak untuk di release sebagai versi terbaru untuk kemudian di merge ke branch master.
c. Setiap Developer ketika membuat sebuah fitur mereka berkolaborasi didalam topic branch dibawah branch development, setelah selesai salah seorang developer melakukan merging dari topic branch ini ke development branch untuk di review bersama.
d. Untuk lebih detail lihat studi kasus.

2. Integration-Manager Workflow
Cara kerjanya adalah sebagai berikut: 



HAL-HAL YANG PERLU DIKETAHUI DI GITHUB:
=======================================
* Cara Forking, dan pull request sederhana bisa di lihat di WPUNPAS #4
* Contoh kasus multiple remote ada di video WPUNPAS #10
* Melakukan perubahan di repo local dan mengajukan perubahan tersebut ke repo yang kita fork ada di video WPUNPAS #11
* Mengupload project ke web hosing menggunakan Git (Menghubungkan Git dengan web hosting) WPUNPAS #14
* Account Setup Configuration
- SSH Access pro git 162
- Setting Avatar
- Setting Email Address
- Setting Two Factor Authentication pro git page 165
setting => security => set up two-factor authentication

* Contributing to Project
- Forking Project => lihat WPUNPAS
- The Github Flow:
	> Fork the project
	> create a topic branch from master
	> make some commits to improve the project
	> push this branch to github project
	> open pull request on github
	> discuss, and optionally continue commiting
	> The project owner merges or close the pull request
- Creating pull request: lihat wpunpas / pro git 167
	> fork the repository
	> clone it locally
	> create a topic branch
	> make the code change
	> push that change back up to github

* Project owner dapat memberi komentari di hasil codingan pada file changes

- Iterating on a pull request, apa maksudnya? 
Jadi setelah melakukan pull request, kemudian ada comment dari project owner dimana po ini menginginkan suatu perubahan supaya pull request di terima, maka contributor bisa memperbaiki code yang di pull request artinya masih bisa melakukan commit di topic branch yang melakukan pull request sehingga pull request nya akan terupdate otomatis dan po akan melakukan merge jika perubahan nya adalah perubahan yang diinginkan oleh po.
NOTES: ketika menambahkan commits di existing pull request, maka tidak akan ada notifikasi yang masuk pada project owner, maka dari itu contributor harus meninggalkan comment untuk me-notice perubahan kepada project owner.
- Apa yang harus dilakukan ketika kita melakukan pull request yang out of date artinya ketika kita melakukan pull request, ternyata code di masternya berubah/ update, sementara code yang ada di pull request kita belum uptodate sehingga warna dari pull request menjadi abu-abu, maka yang harus kita lakukan adalah mengupdate topic branch kita terlebih dahulu, sehingga code kita uptodate dengan code yang ada di remote server baru kita bisa melakukan pull request terhadap perubahan code yang kita lakukan.

* Di github kita bisa melakukan referensi untuk menunjukan issue tertentu, pull request tertentu dsb, untuk lebih jelasnya lihat bagian Reference di pro git 178
* DI github kita bisa menggunakan Markdown (GitHub Flavored Markdown) ketika kita membuat pull request, comment, README.md, CONTRIBUTE.md dsb.
* Menambah Collaborator, pro git 187
Menambah collaborator berarti kita memberikan commit akses kepada collaborator tersebut.
* Pull Request on Pull Reuquest, melakukan pull request pada pull request =>  progit 193
* MEntion di git sama ketika kita melakukan mention di twitter, yaitu dengan menggunakan @
* Setting notification => progit 195
* Special file:
	- README.md => berisi:
		> What the project is for
		> How to conigure and install it
		> An example of how to use it or get it running
		> The license that the project is offered under
		> How to contribute to it


SOP (Workflow) Menggunakan Git Pada Lingkungan Kerja Dengan Sedikit Developer (Centralized Workflow with Private Small Team)
==================================================================
1. Developer 1 membuat repository dengan menambahkan README.md dan file .gitignore yang harus ditambahkan berdasarkan teknologi yang digunakan
2. Developer 1 melakukan installasi framework yang diperlukan dan library-library awal yang dibutuhkan dan melakukan initial commit
3. Developer 1 Membuat 2 buah branch yaitu branch master untuk production dan branch development untuk proses development, dimana setiap ada release baru dari branch development (saat code nya stabil) maka salah seorang Developer melakukan merging dari branch development ke branch master dan menambahkan tag baru untuk release version.
4. Setelah Developer 1 membuat repository dan melakukan initial commit maka Developer lain melakukan clonning di repo local masing-masing
5. Team mengadakan rapat kemudian melakukan pembagian tugas.
6. Masing-masing Developer melakukan pekeraan nya membuat fitur-fitur tertentu di topic branch
7. Setelah fitur selesai setiap developer harus melakukan push branch tempat mengerjakan fitur tersebut ke branch development untuk di review bersama, setelah ok maka developer yang melakukan push topic branch tersebut harus melakukan merging dari topic branch tersebut ke branch development. proses tersebut dilakukan terus-menerus sampai code stabil dan siap di release dan di merging ke branch master.
8. Ketika ada issue di master (revisi dari code production) maka developer harus membuat topic branch dari branch master untuk menyelesaikan issue tersebut setelah issue tersebut selesai developer harus push topic branch tersebut ke remote server kemudian setelah di review dan ok topic branch yang berisi code penyelesaian tersebut di merge ke branch master.

STUDI KASUS WORKFLOW DIATAS
===========================
1. Developer 1 membuat repository di github, menambahkan file README.md dan file .gitignore untuk installasi franework laravel (misal).
2. Semua Developer melakukan cloning remote repository ke local komputer masing-masing
```
	$ git clone https://github.com/IdSundev/latihan-vcs.git
	$ git remote
	$ git remote -V
  ```
3. Developer 1, menambahkan Developer lain nya sebagai collaborator supaya bisa mendapatkan hakakses push, jadi tidak perlu melakukan pull request nantinya. Adapun caranya:
	- Masuk repository nya
	- Klik settings
	- Manage Access
	- Invite Collaborator
	- cari usernamenya
	- add [username] to [repository] 
4. Masing-masing Developer akan menerima email invitation maka klik tombol view invitation dari email tsb, kemudian klik tombol Accept Invitation
5. Semua Developer melakukan configurasi untuk masing-masing account di folder hasil clonning
```
	- Developer 1
	$ git config --list
	$ git config --local user.name "IdSundev"
	$ git config --local user.email chefdeveloper29@gmail.com
	- Developer 2
	$ git config --list
	$ git config --local user.name "cefsyarif"
	$ git config --local user.email cef.syarif@gmail.com
	- Developer 3
	$ git config list
	$ git config --local user.name "cefsh294"
	$ git config --local user.email asep.syarif.294@gmail.com
	- Developer 4
	$ git config --list
	$ git config --local user.name "bokrprtlsmpung29"
	$ git config --local user.email bokrprtlsmpung@gmail.com

	$ git config --local --list
 ```
6. Developer 1 (Ceritanya ya)
```
	- Melakukan installasi laravel
		$ git status
		$ git add .
		$ git commit -m "Installasi framework laravel"
		$ git log
	- Menambahkan library a
		$ git status
		$ git add .
		$ git commit -m "Menambah library A"
		$ git log
	- Menambahkan library b
		$ git status
		$ git add .
		$ git commit -m "Menambah library B"
		$ git log
	- Menambahkan library c
		$ git status
		$ git add .
		$ git commit -m "Menambah library C"
		$ git log
	- Melakukan push ke remote repository
		$ git status
		$ alias = "git log --all --oneline --decorate --graph"
		$ graph => melihat branching
		$ git push origin master
		masukan username
		masukan password
		$ graph
		kode di github sudah uptodate dengan repo local kita
 ```
7. Ceritanya Developer 1 membuat branch Development di repo localnya kemudian membuat file CONTRIBUTOR.md untuk menentukan aturan-aturan kolaborasi, kemudian melakukan commit di branch tersebut dan mempush branch tersebut ke remote repository
```
	$ git branch
	$ git checkout -b development
	$ git branch
	buat file CONTRIBUTING.md
	$ git status
	$ git add .
	$ git commit -m "Membuat branch Development dan membuat file CONTRIBUTING.md"
	$ graph
	$ git push origin development
	masukan username
	masukan password
	$ graph
	Sehingga nanti di remote server nya ada dua branch yaitu branch master dan branch development
```
8. Developer Lain melakukan fetch dari remote server
```
	$ git fetch origin
	$ git status
	$ git branch
	$ git branch -a
	$ graph
```
9. Developer lain menyamakan branch master localnya dengan branch master remote servernya
```
	$ graph
	$ git merge origin/master
	$ graph
```
10. Developer lain membuat branch development di localnya kemudian melakukan merge ke branch origin/development
```
	$ git checkout -b development
	$ git branch
	$ git branch -a
	$ graph
	$ git merge origin/development
	$ graph
```
11. Setelah semua repository dari para developer sama, maka team akan mengadakan meeting untuk pembagian tugas, dan setiap developer harus mengerjakan tugasnya melalui topic branch yang di checkout dari branch development, kemudian saat fiturnya selesai branch tersebut di push ke remote server untuk di review bersama, setelah semua ok maka topic branch tersebut dimerge ke branch development
misal:
	- Developer 1 mendapatkan tugas mengembangkan fiture a
	- Developer 2 mendapatkan tugas mengembangkan fiture b
	- Developer 3 & Developer 4 mendapatkan tugas mengembangkan fiture c

KOMPUTER DEVELOPER 1
====================
- Membuat feature A
```
$ git checkout -b feature_a
$ git branch
$ echo "Menginstall library yang dibutuhkan oleh feature A" > library_feature_a.txt
$ git status
$ git add .
$ git commit -m "Menginstall library yang dibutuhkan oleh feature A"
$ echo "Melakukan coding untuk membuat deature A" > feature_a.txt
$ git status
$ git add .
$ git commit -m "Menambah feature A"
mengirimkan branch feature_a ke remote server dengan nama review_feature_a untuk di review bersama developer lain
$ graph
$ git push origin feature_a:review_feature_a
```
kemudian Developer 1 memberitahukan ke group bahwa feature_a sudah di push ke remote server dengan branch review_feature_a
kemudian Developer lain melakukan fetch ke remote server dan memeriksa hasil code / feature A yang dibuat Developer 1

KOMPUTER DEVELOPER 2
====================
- Membuat feature B
```
$ git branch
$ git status
$ git checkout -b feature_b
$ git branch
$ echo "Menginstall library yang dibutuhkan oleh feature B" > library_feature_b.txt
$ git status
$ git add .
$ git commit -m "Menginstall library yang dibutuhkan oleh feature B"
$ graph
Tiba-tiba pada saat development feature B ada pesan di grup bahwa Developer 1 telah menyelesaikan feature A dan minta untuk di review maka langkah nya adalah:
$ git fetch
$ graph
nah developer 2 ini akan melihat remote branch baru yaitu origin/review_feature_a, maka Developer 2 ini akan melakukan checkout ke branch tersebut untuk melihat kinerja dari feature A
$ git branch
$ git branch -a
$ git checkout origin.review_feature_a
Kemudian Developer 2 dan Developer lain nya akan memeriksa kinerja feature A, dan response dari semuanya setuju dengan kinerja feature A, maka dari itu Developer 2 dan Developer lain nya akan checkout kembali ke topic branch masing-masing
$ git checkout feature_b
$ git branch
$ graph
```

Karena Developer lain telah setuju dengan penambahan feature A, maka Developer 1 harus melakukan merging ke branch development dari branch review_feature_a, dan menghapus branch feature_a yang ada di local dan branch review_feature_a yang ada di remote server
KOMPUTER DEVELOPER 1
====================
```
$ git branch -a
$ graph
$ git checkout development
$ git merge feature_A
$ graph
push code yang telah di merge ke branch development di local ke branch development di remote server
$ git push origin development (pointer masih ada di branch development local ya)
isi username
isi password
$ graph
hapus branch feature_A yang ada di local
$ git branch -d feature_A
$ graph
$ git branch
hapus branch review_feature_a yang ada di remote server
$ git push origin --delete review_feature_a 
$ graph
```
OK sampai sini feature A berhasil dibuat
maka Developer lain harus menyamakan branch development yang ada di remote server dengan branch development yang ada di local mereka
KOMPUTER DEVELOPER 2
====================
```
$ git branch
$ graph
$ git fetch
```
60b8d64..93f1813  development -> origin/development
menandakan ada perubahan di branch development
```
$ graph
$ git checkout development
$ git merge origin/development
$ graph
```
untrack branch review_feature_a dari repo local
```
$ git branch -d -r origin/review_feature_a
```
Developer 2 melanjutkan lagi membuat feature B, nah karena branch development yang ada di remote server sudah di update maka branch feature_b harus uptodate dengan branch origin/development
```
$ graph
$ git branch (pastikan ada di local branch feature_b)
$ git checkout feature_b
$ git merge origin/development
$ graph
```
akan ada auto commit
Merge remote-tracking branch 'origin/development' into feature_b
Lanjutkan membuat feature B
```
$ echo ""
```
UDAH INTINYA AKU GIT, GITHUB, DSB UDAH PAHAM


PELAJARAN:
Sebelum melihat perubahan code yang dilakukan oleh orang lain yang harus kita lakukan adalah membuat branch terlebuh dahulu, baru melakukan git pull
jika terlanjur melakukan git pull ke master, maka lakukan:
git reset --hard <commit dimana kita ingin kembali>
https://stackoverflow.com/questions/17667023/git-how-to-reset-origin-master-to-a-commit

STUDI KASUS:
Misal ada 5 Collaborator yang terdiri dari 2 Maintainer, dan 3 Developer
Ada 3 Fitur yang akan dibangun yaitu Fitur A oleh Developer 1, Fitur B oleh Developer 2, dan Fitur C oleh Developer 3
Scenarionya adalah seperti ini:
- Maintainer 1 Membuat initial project dan melakukan push ke development server
Komputer Maintainer 1
=====================
```
$ git config --local user.email "cef.syarif@gmail.com"
$ git remote add origin https://gitlab.com/mizuko29/studi-kasus-progit.git
$ git add .
$ git commit -m "Initial Commit"
$ git push origin master
```

- Setelah initial commit dibuat, semua collaborator akan melakukan clone dari Remote Repository tersebut
Komputer Maintainer2
====================
```
$ git clone https://gitlab.com/mizuko29/studi-kasus-progit.git
$ git config --local user.email 'maintainer2@karyaalenta.com'
```

Komputer Developer1
===================
```
$ git clone https://gitlab.com/mizuko29/studi-kasus-progit.git
$ git config --local user.email 'developer1@karyaalenta.com'
```

Komputer Developer2
===================
```
$ git clone https://gitlab.com/mizuko29/studi-kasus-progit.git
$ git config --local user.email 'developer2@karyaalenta.com'
```

Komputer Developer2
===================
```
$ git clone https://gitlab.com/mizuko29/studi-kasus-progit.git
$ git config --local user.email 'developer2@karyaalenta.com'
```

- Setelah semua collaborator memiliki Master Branch yang sama dengan Master Branch yang ada di Remote Repository, Maintainer 1 akan membuat 3 Branch yaitu: feature_a, feature_b, dan feature_c dan push branch tersebut ke Master Branch di remote repository.
Komputer Maintainer 1
=====================
```
$ git checkout -b feature_a
$ git checkout master
$ git checkout -b feature_b
$ git checkout master
$ git checkout -b feature_c
$ git checkout master
$ git push origin feature_a
$ git push origin feature_b
$ git push origin feature_c
$ git branch -a
```

- Developer 1, akan menyelesaikan membuat feature_a setelah selesai Developer 1 akan push Branch feature_a ke Branch feature_a yang ada di remote repository dan memberi tahu maintainer untuk memeriksa hasil kerjanya.
Komputer Developer 1
====================
```
$ git branch
$ git checkout -b feature_a
$ // buat file Fitur A.txt
$ git status
$ git add .
$ git commit -m "Sprint1 Fitur A, Developer 1"
$ git push origin feature_a
$ git checkout master
```

- Maintainer 1, akan melakukan pull dari Branch feature_a di lcoal repository miliknya ke Branch feature_a di remote repository dan memeriksa hasil kerja yang dilakukan Developer 1, singkatnya setelah diperiksa ternyata ada yang kurang yang dikerjakan oleh Developer 1, maka Maintainer 1 akan memberitahukan nya ke Developer 1 dan Developer 1 akan memperbaiki code yang dibuatnya.
Komputer Maintainer 1
=====================
```
$ git checkout feature_a
$ git pull origin feature_a
$ // lihat perubahan code, dan menyuruh Developer untuk memperbaiki pekerjaan nya
$ git checkout master
```

- Setelah itu, Developer 2 ternyata sudah menyelesaikan Fitur B nya lalu Developer 2 akan mempush code dari Branch feature_b di local repository nya ke Branch feature_b di remote repository untuk diperiksa oleh Maintainer 1
Komputer Developer 2
====================
```
$ git branch
$ git chekcout -b feature_b
$ // buat file Fitur B.txt
$ git status
$ git add .
$ git commit -m "Sprint1 Fitur B, Developer 2"
$ git push origin feature_b
$ git checkout master
```

- Maintainer 1 akan melakukan pull dari Branch feature_b local ke Branch feature_b di remote repository dan memeriksa hasil kerja Developer 2, setelah memeriksa hasil kerja nya dan sudah sesuai, Maintainer 1 akan melakukan merge ke Branch Master yang ada di local repository miliknya, setelah itu Maintainer 1 melakukan checkout ke Branch Master dan melakukan push ke Branch Master di Remote Repository
Komputer Maintainer 1
=====================
```
$ git checkout feature_b
$ git pull origin feature_b
$ // lihat perubahan code, dan kerjaan nya sudah ok
$ git checkout master
$ git merge feature_b
$ git push origin master
```

- Lalu semua Collaborator akan menyamakan Branch Master local nya dengan Branch Master yang ada di remote 
Komputer Developer 1
====================
```
$ git checkout master
$ git pull origin master
```

Komputer Developer 2
====================
```
$ git checkout master
$ git pull origin master
```

Komputer Developer 3
====================
```
$ git checkout master
$ git pull origin master
```

Komputer Maintainer 2
=====================
```
$ git checkout master
$ git pull origin master
```

- Developer 2, dan Maintainer 1 akan menghapus Branch feature_b di masing-masing local repositorynya dan Maintainer 1 juga akan menghapus Branch feature_b di remote repository
Komputer Developer 2
====================
```
$ git checkout master
$ git branch -d feature_b
$ git branch -a
$ 
```

Komputer Maintainer 1
=====================
```
$ git checkout master
$ git branch -d feature_b
$ git push origin --delete feature_b
$ git branch -a
```

- Develper 3 setelah menyamakan Branch Masternya, Developer 3 pada saat mengerjakan tugas nya akan melakukan pull dari Branch feature_c ke Branch Master yang ada di remote repository supaya Fitur 3 uptodate dengan Master Branch Development Server nya, jika dirasa ada yang confilct Developer 3 akan membetulkan nya kemudian menyelesaikan tugas nya, setelah tugas nya selesai Developer 3 akan Push code yang ada di Branch feature_c di local repository nya ke Branch feature_c yang ada di remote repository untuk diperiksa Maintainer 1
Komputer Developer 3
====================
```
$ git checkout feature_c
$ git pull origin master
$ git status
$ git add .
$ git commit -m "Sprint1 Fitur C, Developer 3"
$ git push origin feature_c
$ git checkout master
```

- Maintainer 1 akan melakukan pull dari Branch feature_c di local repository nya ke Branch feature_c di remote repository dan memeriksa hasil kerja yang dilakukan oleh Developer 3 setelah kerjaan nya dinilai ok, Maintainer 1 akan melakukan merge dari Branch feature_c ke Branch Master local nya kemudian akan melakukan push dari Branch Master Local ke Branch Master yang ada di Development Server(remote repository) setelah itu Developer 1 dan Maintainer 1 akan menghapus Branch feature_c di masing-masing local repository miliknya dan Maintainer 1 akan menghapus Branch feature_c di remote repository.
```
$ git checkout feature_c
$ git pull origin feature_c
$ git checkout master
$ git merge feature_c
$ git push origin master
$ git branch
$ git branch -d feature_c
$ git push origin --delete 
$ git branch -a
```

omputer Developer 3
====================
```
$ git checkout master
$ git pull origin master
$ git branch -d feature_c
$ git branch -a
$ 
```

- Semua collaborator akan melakukan pull dari Branch Master masing-masing ke Branch Master di remote repository
Komputer Developer 1
====================
```
$ git checkout master
$ git pull origin master
```

Komputer Developer 2
====================
```
$ git checkout master
$ git pull origin master
```

Komputer Developer 3
====================
```
$ git checkout master
$ git pull origin master
```

Komputer Maintainer 2
=====================
```
$ git checkout master
$ git pull origin master
```

- Developer 1 di Branch feature_a akan melakukan pull juga ke Branch Master di remote repository untuk menyamakan code nya, kemudian setiap commit yang dilakukan pada Branch feature_a akan di push ke Branch feature_a di remomte repository untuk diperiksa oleh Maintainer 1
Komputer Developer 1
====================
```
$ git checkout feature_a
$ // Mengerjakan fitur a
$ git add .
$ git commit -m "Sprint1 Revisi Fitur A, Developer 1"
$ git pull origin master
$ // merging ke feature_a
$ git push origin feature_a
$ git checkout master
```


- Maintainer 1 akan melakukan pull dari Branch feature_a local ke Branch feature_a remote dan memeriksa hasil tugas Developer 1, jika sudah ok Maintainer 1 akan melakukan Merging dari Branch feature_a ke Branch Master repo local kemudian push dari Branch Master local ke Branch Master remote, kemudian Maintainer 1 dan Developer 1 akan menghapus Branch feature_a di masing masing repo localnya, dan Maintainer 1 akan menghapus Branch fature_a di remote repo.
Komputer Maintainer 1
=====================
```
$ git checkout feature_a
$ git pull origin feature_a
$ git checkout master
$ git merge feature_a
$ git push origin master
$ git branch -d feature_a
$ git push origin --delete feature_a
```

Komputer Developer 1
====================
```
$ git checkout master
$ git pull origin master
$ git branch -d feature_a
```


- Semua Collaborator akan melakukan pull dari Branch Master remote repo ke Branch Master local masing-masing

Komputer Developer 2
====================
```
$ git checkout master
$ git pull origin master
```

Komputer Developer 3
====================
```
$ git checkout master
$ git pull origin master
```

Komputer Maintainer 2
=====================
```
$ git checkout master
$ git pull origin master
```

- Done, Sprint 1 beres!!!

NOTES: Setiap ada perubahan di branch master dev server/ remote repo maka semua branch yang ada harus pull ke origin master















