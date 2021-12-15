# Odoo Experience

- [An In-depth Journey into Odoo's ORM](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/an-in-depth-journey-into-odoo-s-orm-3936) by Raphael Collet
- [Tutorial: Develop App with Odoo Framework](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-01-2622/track/tutorial-develop-an-app-with-the-odoo-framework-3852)
- [The Right Way to Develop Website & eCommerce Features](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/the-right-way-to-develop-website-ecommerce-features-3846)
- [How to Use Custom Code to Handle Upgrades](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/how-to-use-custom-code-to-handle-upgrades-3841)
- [Best Practices in Handling Performance Issues](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/best-practices-in-handling-performance-issues-3857)
- [Odoo's Test Framework: Learn Best Practices](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/odoo-s-test-framework-learn-best-practices-3844)
- [Security: Odoo Code Hardening](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/security-odoo-code-hardening-3853)
- [Best Tools for First-Time Odoo Development](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/best-tools-for-first-time-odoo-development-3862) by Yannick Tivisse: Version Number on odoo.sh, noupdate attribute, IDE, good idea to git merge by hand, Tree Visualizer
- [UX in Business-apps: a-workshop-for-app-developers](https://www.odoo.com/zh_TW/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/ux-in-business-apps-a-workshop-for-app-developers-3858)
- [Running a University with Odoo](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/running-a-university-with-odoo-2058)
- [Odoo Website: How to Develop Building Blocks](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/odoo-website-how-to-develop-building-blocks-3937)
- [Building l10n Payroll Structures from the Ground Up](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/building-l10n-payroll-structures-from-the-ground-up-3861)
- [Empower Your App by Inheriting from Odoo Mixins](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/empower-your-app-by-inheriting-from-odoo-mixins-3860)
- [Preventing user mistakes by using machine learning](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/preventing-user-mistakes-by-using-machine-learning-2171) by Faisal Basar 避免錯誤 員工訓練 學習增長
- [CRM Workshop: Learn How to Manage Your Pipeline](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/odoo-spreadsheet-advanced-features-3915-2622/track/crm-workshop-learn-how-to-manage-your-pipeline-3920) by Nikki Peple Pipeline Probability Studio Qutation Filter GroupBy Analytics Export Deduplication LeadGeneration
- [Say Goodbye to Excel with the New Built-in Odoo Spreadsheets](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/say-goodbye-to-excel-with-the-new-built-in-odoo-spreadsheets-3872) by Brett Hydeman : Better_Business_Intelligence Pivot_Table Commission
- [Odoo Spreadsheet: Advanced Features](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/odoo-spreadsheet-advanced-features-3915) by Nicolas Bassine : Accounting_Pivot Re-insert_pivot
- [Sales Commissions and Dashboard with Odoo Spreadsheet](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/sales-commissions-and-dashboard-with-odoo-spreadsheet-3912) by Devarsh Modi : Sharing 初期只有部分功能
- [Workshop: Budgets and Forecasts with Odoo Spreadsheet](https://www.odoo.com/event/odoo-experience-2020-2020-09-30-2020-10-02-2622/track/workshop-budgets-and-forecasts-with-odoo-spreadsheet-3911) by Eva Lombardo

odoo/addons/base/data/res_country_data.xml
<data noupdate="1">
  <record id="tw" model="res.country">
    <field name="name">Taiwan</field>
    <field name="code">tw</field>
    <field file="base/static/img/country_flags/tw.png" name="image" type="base64" />
    <field eval="'%(country_name)s'"
</data>

[Why the Browser's Debugger is a Backend Developer's Best Friend](http://youtube.com/watch?v=-3UwhYe2HUw)

[Richard Shall](http://www.youtube.com/channel/UCB9cSQS-aB31JXLRw9zQ7-Q): Excel Migration Script 先有測試版本 會再正式推出給昇級用戶

Orgis from Czech 雲端服務 徵求 Python 工程師, [Jana Proskova](http://odoois.com/blog/odoo-2/post/why-is-crm-better-than-excel-36) : CRM 比 Spreadsheet 好的原因
Odoo model XML github.com/Akretion
PySPED

# Dennis Weekend Tutorials

`_name` 如果更改了 資料庫就會直接更新嗎? 或是需要額外通知系統? 如果有填過資料值 也就是有幾筆舊資料了 那前面的 _name 更新動作會被怎樣影響?

name vs code 常成串套用: _rec_name == record name (PO_# 之類)

event/model event_event.py EventType and EventEvent

Many2one One2many Many2oneReference
讀完值才進行 `_compute` 要留意執行效率 store=True


登入記錄 編輯記錄 可以看到時間歷程嗎? 修改 opportunity 標題後 看到前後改成怎樣
QWEB id 如何繼承?
technical 網頁管理介面修改的結果 是否記錄在資料庫裡? 如何清掉 回復成原始設定? 如何匯出 再併進檔案系統的程式碼?


如果是匯出，試著把addons_connector關掉，減少可能的錯誤
可能是這個之類的 https://pypi.org/project/odoo12-addon-connector/

ebsone.com/event/odoo-2020-07-19-20/register
ORM API, View, Action
Web Controller:

docker images
docker search odoo
docker pull odoo
docker run -d -e POSTGRES_USER=odoo
docker start -a odoo
db.sh [docker_script]



Controller 本身是個 Python Class 程式，透過它可以建立網頁或前端程式與 Odoo Module 進行整合，不再侷限於傳統 Form View 或 Tree View 而能呈現自製畫面。

# CRM Controller 範例

[addons/crm/controllers/main.py](https://github.com/odoo/odoo/blob/15.0/addons/crm/controllers/main.py#L12)

from odoo import http

class CrmController(http.Controller):


[整合 chart.js 的舊範例](https://learnopenerp.blogspot.com/2018/08/odoo-web-controller.html)

