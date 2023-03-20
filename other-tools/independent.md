---
description: 此區域的程式碼都為獨立執行的py檔，自行創建純文字文件，複製程式碼貼上後將檔案名改為xxx.py，即可用python執行
---

# 獨立執行

## 應用翻譯轉換

程式目標是將某個omf檔案中的基底語言進行置換，使用前須先修改前四行參數。

例如 test\_flow.omf 是一個以繁體中文設計的應用，已經透過OMFLOW內建的功能上傳過各語言的翻譯，當英語客戶需要此應用借鑒時，可以利用該程式將“設計”的語言從繁體中文改成英文。

{% hint style="warning" %}
請注意，omf檔案中需含有對應翻譯，此程式只是幫您進行翻譯對調，而非自動翻譯。
{% endhint %}

```python
import json


path = '/some_path/test_flow.omf'    #請依照實際路徑及名稱修改
trans_to_path = '/some_path/test_flow.omf'
original_language = 'zh-hant'        #請依照實際需求修改
replace_language = 'ja'



translator_onlytitle_formitem_type_list = ['box12','box6','areabox','n_user','n_group','u_gps','label']
translator_titleplaceholder_formitem_type_list = ['h_title','inputbox','date','datetime','subquery','inputcaculate','file']
translator_lists_formitem_type_list = ['h_level','h_status','list','checkbox']
translator_special_formitem_type_list = ['subtable']

def loopFlowObject(lan_dict, flowobject):
    try:
        items = flowobject.get('items',[])
        for i in items:
            item_type = i['type']
            if item_type != 'line':
                config = i['config']
                
                item_text = lan_dict.get(i['text'],'')
                if item_text:
                    i['text'] = item_text
                
                if item_type in ['start','python','setform']:
                    loop_list = ['input','output']
                    loopInOutPut(lan_dict, loop_list, config)
                
                elif item_type == 'end':
                    loop_list = ['output']
                    loopInOutPut(lan_dict, loop_list, config)
                
                elif item_type in ['outflow','inflow','subflow']:
                    loop_list = ['subflow_input','subflow_output']
                    loopInOutPut(lan_dict, loop_list, config)
                
                elif item_type == 'form':
                    loop_list = ['input','output','subflow_input','subflow_output','input1','input2']
                    loopInOutPut(lan_dict, loop_list, config)
                    
                    action1_text = lan_dict.get(config['action1_text'], '')
                    if action1_text:
                        config['action1_text'] = action1_text
                    action2_text = lan_dict.get(config['action2_text'], '')
                    if action2_text:
                        config['action2_text'] = action2_text
                    
                    form_object = config.get('form_object',{})
                    if form_object:
                        if form_object.get('items',[]):
                            loopFormObject(lan_dict, form_object)
                
                elif item_type in ['async','switch']:
                    pass
    except:
        pass


def loopFormObject(lan_dict, formobject):
    try:
        items = formobject.get('items',[])
        for i in items:
            item_type = i['type']
            config = i['config']
            if item_type in translator_onlytitle_formitem_type_list:
                title = lan_dict.get(config['title'],'')
                if title:
                    config['title'] = title
                
            elif item_type in translator_titleplaceholder_formitem_type_list:
                title = lan_dict.get(config['title'],'')
                if title:
                    config['title'] = title
                
                placeholder = lan_dict.get(config['placeholder'],'')
                if placeholder:
                    config['placeholder'] = placeholder
                
            elif item_type == 'h_group':
                group_title = lan_dict.get(config['group_title'],'')
                if group_title:
                    config['group_title'] = group_title
                
                user_title = lan_dict.get(config['user_title'],'')
                if user_title:
                    config['user_title'] = user_title
                
            elif item_type in translator_lists_formitem_type_list:
                title = lan_dict.get(config['title'],'')
                if title:
                    config['title'] = title
                
                lists = config['lists']
                for l in lists:
                    text = lan_dict.get(l['text'],'')
                    if text:
                        l['text'] = text
        
            elif item_type in translator_special_formitem_type_list:
                title = lan_dict.get(config['title'],'')
                if title:
                    config['title'] = title
                
                loopFormObject(lan_dict, config['form_object'])
    except:
        pass


def loopInOutPut(lan_dict, loop_list, config):
        try:
            for i in loop_list:
                n_lst = config[i]
                for n in n_lst:
                    des = lan_dict.get(n['des'],'')
                    if des:
                        n['des'] = des
        except:
            pass



try:
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
        f.close()
    omf_list = json.loads(content)
    for omflow_app_dict in omf_list:
        this_app_language_package = omflow_app_dict.get('language_package',{})
        this_app_language_package = json.loads(this_app_language_package) if isinstance(this_app_language_package, str) else this_app_language_package
        zh_hant = this_app_language_package.get('zh-hant',{})
        en = this_app_language_package.get('en',{})
        ja = this_app_language_package.get('ja',{})
        zh_hans = this_app_language_package.get('zh-hans',{})
        replace_dict = this_app_language_package.get(replace_language,{}).copy()
        this_app_name = replace_dict.get(omflow_app_dict.get('app_name',''),'')
        if this_app_name:
            omflow_app_dict['app_name'] = this_app_name
        this_app_flow_list = omflow_app_dict.get('flow_list',{})
        for flow in this_app_flow_list:
            this_flow_name = replace_dict.get(flow['flow_name'],'')
            if this_flow_name:
                flow['flow_name'] = this_flow_name
            this_description = replace_dict.get(flow['description'],'')
            if this_description:
                flow['description'] = this_description
            
            this_flowobject = flow.get('flowobject',{})
            loopFlowObject(replace_dict, this_flowobject)
            this_formobject = flow.get('formobject',{})
            if not this_formobject:
                this_formobject = this_flowobject.get('form_object',{})
            loopFormObject(replace_dict, this_formobject)
            
            this_subflow_list = this_flowobject.get('subflow',[])
            for subflow in this_subflow_list:
                this_subflow_name = replace_dict.get(subflow['name'],'')
                if this_subflow_name:
                    subflow['name'] = this_subflow_name
                this_subflow_description = replace_dict.get(subflow['description'],'')
                if this_subflow_description:
                    subflow['description'] = this_subflow_description
                loopFlowObject(replace_dict, subflow)
        
        new_dict = {}
        new_lan = ''
        for origin_text in replace_dict:
            replace_text = replace_dict[origin_text]
            if replace_text:
                if origin_text in zh_hant:
                    trans_text = zh_hant.pop(origin_text)
                    zh_hant[replace_text] = trans_text
                    if replace_language == 'zh-hant':
                        new_dict[replace_text] = origin_text
                if origin_text in en:
                    trans_text = en.pop(origin_text)
                    en[replace_text] = trans_text
                    if replace_language == 'en':
                        new_dict[replace_text] = origin_text
                if origin_text in ja:
                    trans_text = ja.pop(origin_text)
                    ja[replace_text] = trans_text
                    if replace_language == 'ja':
                        new_dict[replace_text] = origin_text
                if origin_text in zh_hans:
                    trans_text = zh_hans.pop(origin_text)
                    zh_hans[replace_text] = trans_text
                    if replace_language == 'zh-hans':
                        new_dict[replace_text] = origin_text
        
        this_app_language_package[original_language] = new_dict
        omflow_app_dict['language_package'] = json.dumps(this_app_language_package)

    result = json.dumps(omf_list)
    
    with open(trans_to_path, "w", encoding="utf-8") as f:
        f.write(result)
        f.close()
except Exception as e:
    print(e.__str__())


```



