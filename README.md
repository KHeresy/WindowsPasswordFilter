# WindowsPasswordFilter

這是一個基於微軟 V2 Credential Provider Sample 修改出來的 Windows 8+ 登入介面。
他的功能是用來應付某些單位無腦的密碼長度需求，可以在既有密碼的後面，加入任意長度的字元，來做密碼長度的偽裝。

## 安裝方法

將 PwdFilterCredentialProvider.dll 和 PwdFilterCredentialProvider.ini 複製到 C:\Windows\System32 下，然後再執行 register.reg 即可。

這兩個步驟都需要系統管理者權限，安裝後不須重開機。

## 移除方式

只需要將 PwdFilterCredentialProvider.dll 和 PwdFilterCredentialProvider.ini 刪除，並執行 Unregister.reg。

## 使用方法

安裝完成後，在 Windows 的登入、鎖定畫面，在輸入密碼的下方，會多出「登入選項」，點選之後，可以選擇登入的方法。
在點選新的登入方式後，即可按照一般的方法，輸入密碼完成登入。

這邊的差別在於：
* 指定的「中斷字元」（預設為「-」）後輸入的字元，會顯示在畫面上，但是在實際送出時，會被濾掉。

      例如，密碼輸入「abcd-123456」的話，實際上送給系統的會是「abcd」，但是顯示的長度還是會是 11 個字元。

* 如果在輸入「中斷字元」時，螢幕所顯示的密碼長度還不到指定的長度（預設為 16），會自動加長到指定長度。

      例如，密碼輸入「abcd-」，由於長度不到 16，所以會被自動補成「abcd------------」共 16 個字元，但是當按下確定登入時，送給系統的還是只有「abcd」。

中斷字元和指定長度可在 PwdFilterCredentialProvider.ini 中修改。
PwdFilterCredentialProvider.ini 第一行的第一個字元即為中斷字元，預設為「-」；指定長度則為第二行的數字，預設為 16。

## 參考資料

* https://code.msdn.microsoft.com/windowsapps/V2-Credential-Provider-7549a730
* https://kheresy.wordpress.com/2015/09/18/something-about-credential-provider-framework/
