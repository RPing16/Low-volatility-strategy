# Low volatility strategy
將低波動策略應用於台股，每日買進過去D天累積波動最小的前N檔股票，權重依據當日波動進行加權

# files
1. **Low volatility.ipynb**
- 低波動策略code
2. **Strategy performance analysis.html**
- 低波動策略績效分析code
3. ****Strategic Performance Analysis Chart**
- 低波動策略績效分析圖表

## data
- benchmark : 台灣加權股價指數(Y9999)
- Strategy : 台灣所有上市上櫃公司
- 類別 : 報酬率資料
- 時間 : 2010/01/01 ~ 2023/06/30
- sources : TEJ

## 內容摘要
1. **讀取並處理data**
2. **設計低波動策略**
3. **回測**
4. **參數最佳化**
5. **檢驗每日持股數量是否有成功固定住**
6. **使用最佳參數生成分析圖表**

## 結論
- 期間 : 波動策略績效長期優於短期
- 適用性 : 扣除交易成本後最大sharpe ratio = 1.7，績效不錯，說明低波動策略適用於台股
  
## code重點說明
1. **normalize**
- 計算每日股票持有權重時進行標準化，依據當日跌幅進行加權
2. **signal**
- signal>=0，signal>0買進持有，signal=0不持有。signal>0的幅度愈大，持有權重愈大
3. **參數最佳化 - days**
- 使用不同參數days，尋找哪個days使策略sharpe ratio極大
- 結果 : 波動策略績效長期優於短期

## 策略績效分析圖表

- 結果 : 長期低波動策略績效明顯優於長期
5. **其他分析 : 比例 -> 固定數量**
- 本project主要是採取買進『固定比例』的股票，因此當買進比例設定較大(threshold較小)時，會使得股票週轉率大幅增加 -> 交易成本大增 -> 策略報酬下降
- 因此，額外提供是以買進『固定數量』股票的code，透過降低股票週轉率降低交易成本

