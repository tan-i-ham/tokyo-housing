## Library Requirement
`pip install scrapy`

## Target Website Analysis
https://www.homes.co.jp/chintai/

* AJAX

every click(condition, change some of the request formdata)
use **Chrome Developer Tools** & **[cURL syntax converter](https://curl.trillworks.com)** to know the details of request

```json=
data = {
  'cond[roseneki][88205053]': '88205053', # 學藝大學
  'cond[roseneki][88205054]': '88205054', # 都立大學
  'cond[monthmoneyroom]': '0', # 賃料： 下限 （萬）
  'cond[monthmoneyroomh]': '15', # 賃料： 上限 （萬）
  'cond[kanrihi]': '1', # 含管理費
  'cond[housearea]': '30', # 下限：30平方米
  'cond[houseareah]': '0', # 上限：沒設定
  'cond[madori][13]': '13', # 間取り : 1DK
  'cond[madori][15]': '15', # 間取り : 1LDK
  'cond[madori][23]': '23', # 間取り : 2DK
  'cond[walkminutesh]': '15', # 駅徒歩分
  'cond[houseageh]': '10',  # 十年
  'bukken_attr[category]': 'chintai', # rent
  'bukken_attr[pref]': '13', # prefecture: tokyo
  'bukken_attr[rosen]': '882' # train line code: 東急東橫線
}
```

## Play in Scrapy Shell 
> wanna know the house of 1LDK average price bewtween my target station (shibuya ~ jiyugaoka) 


```python=
#### in scrapy shell

url="https://www.homes.co.jp/chintai/tokyo/tokyutoyoko-line/list/"

headers = {
    'cookie': 'D_ZID=2E549B7C-8A5E-3278-8C3F-DE680054DE35; D_ZUID=EB1E65FD-3B1C-3AA0-AC64-9811CF638618; D_HID=5CBFEF2F-8F2F-3DCA-AC91-BA76C037729A; D_SID=36.2.2.190:hb5ouxiFnF+yiiRFILlvhIJx0etvPSN70hUjR89bbyQ; c_session=63b752db85bd5df67d9ee8473c40e57d; euid=70e117e9-36ea-4e82-94fe-07a3801ba8e8; c_popup_new_arrival=1561988453; c_nextra_individual_uid=bda5aa799f07c4287d53507f58e8c9b520449213015d1a0d653f117; TS018f23e9=01c857bb1c9a1f1c58486258cf20f86a0f32f77bf07075dd1115f8ea33e32d28a9e17f264d26f2f77ce80990388dead72933a57706abcf13f198189815b1a52c9bb3b1873ffd3d6538095b13bedb44cae26584f4fd51cc8b66938ddb6555313ee6ae63f9ad993bd4640e6508c640556fde6a875f9fde892dd3a2d446c5c74f07f5855992c7a1dc1aa11003118288876ddfebec6ff2462fac141bba97f2596e14b95552464d; c_dsp_ab=a21b33c17d32e50f08g32h40i25j53; cX_S=jxkfl8pf5kobdv9g; cX_P=jxkfl8pk597b65af; IID=2886dbe2566843719723b38f80fccddb; _ga=GA1.3.620734441.1561988444; _gid=GA1.3.1777605305.1561988444; _atrk_siteuid=cdxSFbtR6m8VH1IO; c_im_set=1; c_ga_im_set=1; krt.vis=1393995782_1561988444308_653691668; _fbp=fb.2.1561988444387.1617618682; __ara_uid#45b6ef913dc5feb7=s6C6f7wpd2vxS83qZ6XoXpXHm2ryfset; _ra=1561988444884|c4bd11d4-318f-4dd6-8a70-5f2478e62e8c; _a1_f=d97c8f9e-70ec-401c-bfc1-daef4fc360da; cX_G=cx%3A2e2pjo3ds2fen3fz5xp3129whq%3A5bkse326i84l; _tac=false~self|not-available; _ta=id~1~bb190333f04a1f2a0d947126d10ac917; __ara_sync#adlogue=1; __ara_sync#reckoner=1; _a1_u=befca6a7-548f-4c04-9d3c-f4a4dce77f90; cto_lwid=ea00aded-f66f-422c-94b6-272608f3ee75; appier_utmz=%7B%22csr%22%3A%22www.homes.co.jp%22%2C%22timestamp%22%3A1561988444%2C%22lcsr%22%3A%22www.homes.co.jp%22%7D; D_IID=C70A305B-B7D4-35A9-BDBE-A51FE5E0CDAD; D_UID=7E971B6A-87E8-3C6D-9456-80557F571BE8; __hd_ss=1562016407808; _atrk_ssid=gCcAHzWZ7dPCLgWenCb_qz; __ara_sessid#45b6ef913dc5feb7=b52246233ec7450c9edff1f0bc0b5966_1562016422; _tas=e07mvm7szo; c_ga_hi_cha=chintai; c_ga_hi_mbg=ch; cstp=604800; c_ga_hi_rot=rosen; TS01ec9519=01c857bb1c7684718aec755f547fcf1e89514ce37d4b0d7e0a8821c49f278d4c207e918139bee02de91c23e461dac7f1dae257550a9c99c283f3fd5e337bb2cda848cfda9a4ac5f45732333caf3669364309bbda6e0de52e54a0c1ed0f91b2acd1b58b40201ea5f08ce579df2e9204819753e151c7325585701140f9a325881ac02d2cd22c25c59dfe0c1b7e7699a370af0f0db53bb48ff8384f4036144028feada123d7537468fd78b9986ca3de5637505153603373dbaaec838e52f7e333535c3188e986b8412b1715a30b18953172ea6cf2906473de49f2d7f81ce6d20049d812d0bb415ffa02c8978d67f7e5f3715d886d04fa; TAGKNIGHT_CONTROL_CLUSTER=92; _td=0d8e88dc-944b-4de3-abaa-8bce83d80980; _atrk_sessidx=9; __ara#45b6ef913dc5feb7=eNqrVioozUxRssorzcnRUUouKMpMToXx4pOVrKprawHa5Awj',
    'origin': 'https://www.homes.co.jp',
    'accept-encoding': 'gzip, deflate, br',
    'accept-language': 'zh-TW,zh;q=0.9,en-US;q=0.8,en;q=0.7,zh-CN;q=0.6,la;q=0.5,ja;q=0.4,lb;q=0.3',
    'x-requested-with': 'XMLHttpRequest',
    'x-distil-ajax': 'tsbrfqzewrtwtdxduseqefcv',
    'pragma': 'no-cache',
    'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.131 Safari/537.36',
    'content-type': 'application/x-www-form-urlencoded',
    'accept': 'application/json, text/javascript, */*; q=0.01',
    'cache-control': 'no-cache',
    'authority': 'www.homes.co.jp',
    'referer': 'https://www.homes.co.jp/chintai/tokyo/tokyutoyoko-line/list/',
}

data = {
  'kks[0][id]': 'kksSid',
  'kks[0][adtype]': 'usual',
  'kks[0][key]': '030:00:00:000:0000000000',
  'kks[0][lmt]': '3',
  'kks[1][id]': 'kksSideFeature',
  'kks[1][adtype]': 'usual',
  'kks[1][key]': '040:00:00:000:0000000000',
  'kks[1][lmt]': '3',
  'cond[sortby]': 'recommend',
  'cond[precond]': '3000',
  'referer': 'list',
  'landingRouteAttr': 'a:4:{s:8:"category";s:7:"chintai";s:4:"pref";i:13;s:5:"rosen";i:882;s:6:"_route";s:31:"bukken_list_category_pref_rosen";}',
  'totalhits': '654',
  'cond[pref]': '13',
  'cond[rosen][882]': '882',
  'cond[roseneki][88200578]': '88200578',
  'cond[roseneki][88205050]': '88205050',
  'cond[roseneki][88205051]': '88205051',
  'cond[roseneki][88205052]': '88205052',
  'cond[roseneki][88205053]': '88205053',
  'cond[roseneki][88205054]': '88205054',
  'cond[roseneki][88205055]': '88205055',
  'cond[mbg][3002]': '3002',
  'cond[mbg][3001]': '3001',
  'cond[mbg][3003]': '3003',
  'cond[monthmoneyroom]': '0',
  'cond[monthmoneyroomh]': '0',
  // 'cond[kanrihi]': '1',
  'cond[housearea]': '0',
  'cond[houseareah]': '0',
  'cond[madori][15]': '15', # 1LDK
  'cond[walkminutesh]': '0',
  'cond[houseageh]': '0',
  'cond[newdate]': '0',
  'cond[freeword]': '',
  'cond[fwtype]': '1'
}

req = FormRequest(url, headers = headers, formdata=data)
fetch(req)
view(response)

```