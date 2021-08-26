**憑證破解流程:**  
1. 進入 licence-create 執行 docker-compose up 生成 gitalb-ee licence 相關憑證
2. 將此 license_pub.key 掛入相對應位置,如 docker-compose.yaml 設定
3. 進入 gitlab 網頁 url範例-> https://localhost/admin/license 上傳 GitlabBV...檔案
(步驟4,不做也沒關係,用不到那麼大)
4. 修改 gitlab container 內此檔案-> /opt/gitlab/embedded/service/gitlab-rails/ee/app/models/license.rb
   此行 restricted_attr(:plan).presence || STARTER_PLAN ---> restricted_attr(:plan).presence || ULTIMATE_PLAN 

**參考網址:**
https://blog.starudream.cn/2020/01/19/6-crack-gitlab/

**備註:**  
憑證的部分放在 cert 資料夾裡面，上傳至 gitlab 上有加密過，此憑證為目前GCP上的共用憑證，需小心保管。  
解鎖指令範例 git-crypt unlock ../git-crypt-key  
git-crypt-key 這隻檔案找 lid_chen 拿。  

**Google IAP 操作 Gitlab VM 機器相關指令:**  

- **Port Forward + Git Clone SSH**  
`gcloud compute start-iap-tunnel gitlab 22 --zone asia-east1-b --project gcp-20210526-001 --local-host-port=localhost:10022`  
`git clone ssh://git@localhost:10022/gitlab-instance-ad6063b3/monitoring.git`
- **SCP**  
`gcloud compute scp --recurse gitlab gitlab:~/ --zone asia-east1-b --project gcp-20210526-001 --tunnel-through-iap —port 222`  
- **SSH**  
`gcloud compute ssh gitlab --zone asia-east1-b --project gcp-20210526-001 --tunnel-through-iap -- -p 222`
