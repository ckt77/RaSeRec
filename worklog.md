2024/04/20:
建立環境，發現直接執行指令"pip install -r requirements.txt"會有版本衝突之問題。
後來解決方案: 建立新的文件"requirements_py39.txt"，並建立環境"raserec-env"。

2024/04/21:
腳本"raserec.sh"的第一行指令執行後會輸出如:
'DuoRec' object has no attribute 'presetting_ram'
的報錯訊息；這是因為在"quick_start.py"中只有當config['model'] == 'RaSeRec'時，才會
定義並使用特定的函式。因此，需要進行以下修改(共兩處修改):
-------------------------------------------------------------------------------
if config['model'] == 'RaSeRec':
    model.presetting_ram()
    model.precached_knowledge()
-------------------------------------------------------------------------------
if config['model'] == 'RaSeRec':
    model.precached_knowledge_val(valid_data)
-------------------------------------------------------------------------------

在腳本"raserec.sh"中有記述，需要先進行第一階段的Collaborative-based Pre-training，
然後將Pre-training的結果紀錄(check point路徑)，並用於第二階段的Retrieval-Augmented 
Fine-tuning。