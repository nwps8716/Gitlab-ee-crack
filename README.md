**憑證破解流程:**  
1. 進入 licence-create 執行 docker-compose up 生成 gitalb-ee licence 相關憑證
2. 將此 license_pub.key 掛入相對應位置,如 docker-compose.yaml 設定
3. 進入 gitlab 網頁 url範例-> https://localhost/admin/license 上傳 GitlabBV...檔案
(步驟4,不做也沒關係,用不到那麼大)
4. 修改 gitlab container 內此檔案-> /opt/gitlab/embedded/service/gitlab-rails/ee/app/models/license.rb
   此行 restricted_attr(:plan).presence || STARTER_PLAN ---> restricted_attr(:plan).presence || ULTIMATE_PLAN 

**參考網址:**
https://blog.starudream.cn/2020/01/19/6-crack-gitlab/ 
