# 資料庫復原

database restore error access denied 通常代表 Master Password 錯誤，把 odoo-server.conf 的 admin_password 修改後就可以匯入。
以 mydb-20201001.zip 備份檔案為例，匯入時可以指定新資料庫名稱，例如 yourdb 就可以避免重覆。

# 客戶名單

合併: 春嬌建立了一筆 Individual 名稱是谷歌公司，填了電郵，並在客戶關係裡建立 Opportunity，系統記錄 ID 是 2581。志銘想要透過合併方式來修訂，先建立一筆 Company 名稱是谷歌公司，其他欄位都未填，系統記錄 ID 是 2596。選擇這兩筆在執行合併時，要先指定 Destination Contact 是志銘的資料，因為志銘資料是新的，下拉選單裡要選擇下方項目。合併結果的編輯記錄呈現，最早建立者還是春嬌，接著記錄志銘的建立時間，再記錄春嬌的 Opportunity 時間，最後是合併時間和內容像 Merged with the following partners: 谷歌公司 <some@gmail.com> (ID 2581)。

Opportunity 客戶選 Company 時，Contact 裡 Company 的 Opportunity 單獨會加總，客戶選 Inidividual 時，Company 和 Individual 都會同時加總。也就是說，有歸戶到 Company 的效果。

# 資料匯入與匯出

以 CRM 為例，它的範例 crm_lead.xls 可能版本過舊，目前懷疑不適用。
匯入流程測過 CSV 和 XLSX 格式，都成功?

在 Export Data 勾選 I want to update data 指定 CSV 匯出格式，從 Available Fields 把 Activites 加進 Fileds to Export。匯出的結果顯示 activity_ids 欄位的值是像 Send Proposal 這樣，證實此處的 ids 是指 title 之意。再把相關細節欄位都匯出後，就容易找到需要的資訊：
Activities | activity_ids: Send Proposal
Activities/Activity Type | activity_ids/activity_type_id: Email
Activities/Activity Type/External ID | activity_ids/activity_type_id/id: mail.mail_activity_data_email
Activities/Activity Type/Name | activity_ids/activity_type_id/name: Email
Activities/Due Date | activity_ids/date_deadline: 2020–06–01
Activities/External ID | activity_ids/id: __export__.mail_activity_22_fdab3f8c
Activities/Note | activity_ids/note: <p>To see if this record will appear.</p>

# 搜尋條件的領域設定

crm_lead.py

    partner_id = fields.Many2one('res.partner', string='Customer', tracking=10, index=True,
        domain="['|', ('company_id', '=', False), ('company_id', '=', company_id)]", help="Linked partner (optional)...
    
    partner_id = fields.Many2one('res.partner', string='Customer', tracking=10, index=True,
        domain="['&', ('name', 'not like', '360d'), ('company_id', '=', company_id)]", help="Linked partner (optional)...

搜尋 Customer 時，只會找 360d 的人員。

        domain="['&', ('name', 'not like', '360d'), ('company_id', '=', company_id)]",

只剩 360d 公司

# 網頁樣版的復原

在 Template ID: website.homepage 的 <div id="wrap" class="oe_structure oe_empty"/> 下方新增 JavaScript 嵌入碼，可以正常生效。

    <t name="Homepage" t-name="website.homepage1">
        <t t-call="website.layout">
            <t t-set="pageName" t-value="'homepage'"/>
            <div id="wrap" class="oe_structure oe_empty"/>
    <div id="comboWidgetContainer"></div>
    <script src="https://api.caas.tw/Widget/Layout.js"></script>
    <script>
       var widget = new OnePage.Layout({"Container":"comboWidgetContainer","Id":337,"Key":"rZhiGTJWK5iHHL5yOQGRcILZDIaYwh2c2FEY0u8a65k%3d","EmbeddedType":"OnePage.EmbeddedType.div","Language":"zh-TW","LayoutId":3});
    </script>
    <hr></hr>
            </t>
        </t>

website.homepage 是在 https://github.com/odoo/odoo/blob/13.0/addons/website/models/website.py#L207 由 `_bootstrap_homepage()` 產生，並會指定 priority 值。
