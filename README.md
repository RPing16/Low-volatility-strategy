# Low volatility strategy
將低波動策略應用於台股，每日買進過去D天累積波動最小的前N檔股票，權重依據過去累積波動進行加權，波動度愈低權重愈大

## 動機 
- 過去文獻指出，低波動策略因承擔較小的風險，在風險調整後普遍獲得較高的報酬
- 過去實證研究為美股，好奇在台股是否也會有同樣結果
- 參考文獻 : https://www.robeco.com/en-hk/glossary/quantitative-investing/low-volatility-anomaly

## files
1. **Low volatility.ipynb**
- 低波動策略code
2. **Strategy performance analysis.html**
- 低波動策略績效分析code
3. ****Strategic Performance Analysis Chart**
- 低波動策略績效分析圖表

## data
- benchmark : 台灣加權股價指數(Y9999)
- Strategy : 台灣所有上市上櫃公司
- 類別 : 日報酬率資料
- 時間 : 2010/01/01 ~ 2023/06/30
- sources : TEJ

## 交易成本
台股目前券商手續費有優惠，普遍有6折，部分券商提供1~2.8折優惠。若以3折優惠計算:
- 手續費 : 0.1425%*0.3，買賣都收
- 證交稅 : 0.3%，賣出才收
- 買入交易成本 = 0.1425%*0.3 = 0.04275%
- 賣出交易成本 = 0.1425%*0.3 + 0.3% = 0.34275%
- total交易成本 = 0.3855%
- 平均total交易成本 = 0.19275%
- 本專案交易成本計算方式採「單邊0.2%」

## 內容摘要
1. **讀取並處理data**
2. **設計低波動策略**
3. **回測**
4. **檢驗每日持股數量是否有成功固定住**
5. **報酬貢獻度分析**
6. **參數分析**
7. **使用最佳參數生成分析圖表**

## 結論
- 低波動策略在台股也良好的績效，與美股實證研究結論相同
- 低波動策略在長期表現較好，在參數days=235天時達到最高sharpe ratio = 1.59
  
## code重點說明
1. **rank**
- 在計算signal時，給予波動度rank以轉換原始訊號 : 波動度數值 -> 波動度rank (波動度愈低rank愈高)
- 用意 :
    - 使用原始信號分配權重可能發生權重過度集中在某幾個股票(離群值)
    - 為降低風險，將原始信號轉換成rank，如此一來，既保留原始訊號的大小順序關係，又可以控制住權重不會過度集中
- 正面效果 : 降低策略風險，使策略報酬不易受離群值影響，同時使得策略報酬貢獻度較平均
2. **signal**
- signal>=0，signal>0買進持有，signal=0不持有。signal>0的幅度愈大，持有權重愈大
3. **normalize**
- 計算每日股票持有權重時進行標準化，依據當日波動度rank進行加權
  
## 策略績效分析圖表
![示例圖片](https://github.com/RPing16/Low-volatility-strategy/blob/main/Strategic%20Performance%20Analysis%20Chart/cum%20ret%20line%20chart.jpg)

![示例圖片](https://github.com/RPing16/Low-volatility-strategy/blob/main/Strategic%20Performance%20Analysis%20Chart/key%20performance%20table.jpg)

![示例圖片](https://github.com/RPing16/Low-volatility-strategy/blob/main/Strategic%20Performance%20Analysis%20Chart/EOY%20Returns%20vs%20Benchmark.jpg)

![示例圖片](https://github.com/RPing16/Low-volatility-strategy/blob/main/Strategic%20Performance%20Analysis%20Chart/rolling%20index.jpg)
