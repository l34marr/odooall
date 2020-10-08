Opportunity 客戶選 Company 時，Contact 裡 Company 的 Opportunity 單獨會加總，客戶選 Inidividual 時，Company 和 Individual 都會同時加總。也就是說，有歸戶到 Company 的效果。

database restore error access denied 通常代表 Master Password 錯誤，把 odoo-server.conf 的 admin_password 修改後就可以匯入。

crm_lead.py

    partner_id = fields.Many2one('res.partner', string='Customer', tracking=10, index=True,
        domain="['|', ('company_id', '=', False), ('company_id', '=', company_id)]", help="Linked partner (optional). Usually created when converting the lead. You can find a partner by its Name, TIN, Email or Internal Reference.")
    
    partner_id = fields.Many2one('res.partner', string='Customer', tracking=10, index=True,
        domain="['&', ('name', 'not like', '360d'), ('company_id', '=', company_id)]", help="Linked partner (optional). Usually created when converting the lead. You can find a partner by its Name, TIN, Email or Internal Reference.")

搜尋 Customer 時，只會找 360d 的人員。

        domain="['&', ('name', 'not like', '360d'), ('company_id', '=', company_id)]",

只剩 360d 公司

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
