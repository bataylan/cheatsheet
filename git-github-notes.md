# Git Komutlarim

Make one commit per logical changes, not for every line or too long periods.

Branch degistirme `git checkout branch_name`

Add all files to commit `git add .`

Commit changes `git commit -m "Commit message (Start with Add/Update/Fix/Delete)"`

Push `git push origin branch_name`

Rebasing local commits `git rebase --interactive HEAD~7`

Linux ve MacOS 'da iki dosya arasındaki farklıları gösterme komutu `diff -u` 

## Projede calisirken genel siralama

`git fetch --all` tum guncellemeleri alma

`git checkout branch_name` branch degistirme

**Degisiklik yaptiktan sonra**

`git status` ile kontrol etme

`git add .` ile olusturulan dosyalari ekleme

`git commit -m "Commit message"` ile yapilan degisiklikleri commitleme

`git push origin branch_name` ile yapilan degisiklikleri Github/Gitlab vb. servise gonderme

## Stash kullanimi

`git stash` ile yapilan degisiklikler stashlenebilir

`git stash list` ile stashlerin listesini gorme

`git stash apply` ile stashleri changes olarak apply etme veya `git stash apply stash@{STASH_INDEX}` ile belirli bir stash'i apply etme.


## Merge
`git checkout master`

`git fetch --all`

`git merge branch_name --no-commit --no-ff`

IntelliJ -> Right Click -> Git -> Solve conflicts

`git merge --continue`

**Yapilan degisiklikler ile ilgili varsayilan text editorunu acicak, kapattiktan sonra merge islemi tamamlanmis oluyor**

`git push origin master`

## Submodule ler ile calisma

`git submodule update --init` projeyi clone ladiktan sonra submodule leri cekmek icin kullanilan komut

`git submodule add <git-url>` submodule'u bulunulan klasore eklemek icin kullanilan komut

submodule silmek icin kullanilan komut

```
git submodule deinit <asubmodule>    
git rm <asubmodule>
```

Submodulelerde pull yapilamiyorsa (head detached oldugu icin) `git checkout main` ile main branchine gecip pull yapilabilir.

## Git amend

`git commit --amend --date=now --no-edit` mevcut commitin tarihini değiştirme

## Git-crypt

Bu tool'un herhangi bir gizli bilgi repository e eklenmeden kullanilmasi gerekiyor, yoksa gizli bilgi bir kez git ile eklendiginde gecmisten hep gozukecektir.

Gerekli cli toollar yuklu mu kontrol etmek icin `gpg --version`, `git --version`

Kisisel anahtarimizi uretmek icin tam uretim proseduru baslatma `gpg --full-generate-key` (varsayilan RSA and RSA -> 3072 -> 1y)

Uretilen key'in public idsini alma `gpg --list-keys` kodunda ilgili key'de pub satirinin alt satirinda yazar rakam ve harfler.

Uretilen key'i exportlama `gpg --armor --export --output GPG-DIRECTORY-PATH/KEY-NAME.gpg PUBLIC-KEY-ID`

Kurulum icin komutlar, oncelikle yeni bir branche gecmek iyi bir fikir `git branch security-init` ve `git checkout security-update`.

Git-crypt'in gerekli dosyalari olusturmasi `git-crpyt init`

Git-crypt'e ilgili kullanicinin sifre anahtarini ekleme `git-crypt add-gpg-user PUBLIC-KEY-ID`

Eger yoksa .gitattributes dosyasi olusturulmali

.gitattributes dosyasinin icerisinde sifrelenecek dosyalarin oldugu klasoru belirtme

```
FOLDER-PATH-TO-CRYPT/** filter=git-crypt diff=git-crypt
```

git-crypt otomatik olarak pull ve push aksiyonlarinda dosyalari sifreleyecek ve geri acacaktir. 

Test etmek icin `git-crypt lock` komutu kullanildiktan sonra dosyalar sifrelenmis mi diye kontrol edilip, ardindan `git-crypt unlock` komutu ile dosyalar geri acilir.
 

## Kullanmaktan kacinilmasi gereken komutlar

Git ile bir dosyayi kalici olarak silme (gecmis de dahil) `git filter-branch --index-filter "git rm -rf --cached --ignore-unmatch FILE-PATH" HEAD`.

## Git'in command line'ı renklendirme ayarı

```
git config --global core.editor "'/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl' -n -w"
git config --global push.default upstream
git config --global merge.conflictstyle diff3
```
