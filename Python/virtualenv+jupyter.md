Python Virtualenv with Jupyter Notebook
===
## Execution Policy
使用 PowerShell 執行自定 script 檔，卻出現「檔案無法載入，因為這個系統已停用指令碼執行」的訊息，表示在目前作業系統中的執行原則 ( Execution Policy ) 預設狀態為 Restricted，也就是不允許執行。  
  
可透過一些指令進行執行原則變更，首先請用管理員權限打開 PowerShell，執行以下指令：

```
> Set-ExecutionPolicy RemoteSigned
```

## Jupyter notebook with venv
在 virtualenv 中安裝 `ipython`

```
> .\env\Scripts\activate    # start your virtualenv
> pip install ipykernel
```

把 virtualenv 中的 python 環境安裝至 ipython kernel

```
> python -m ipykernel install --user --name=your_virtualenv_name
```
