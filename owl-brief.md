# Let's Build a To-do List

http://github.com/ged-odoo/owl-todolist

## Adding the First Component

    const { Component } = owl;
    const { xml } = owl.tags;
    const { whenReady } = owl.utils;
    
    // OWL Components
    class App extends Component {
      static template = xml`<div>todo app</div>`;
    }

    // Setup Code
    function setup() {
      const app = new App();
      app.mount(document.body);
    }

    whenReady(setup);

## Displaying Tasks

    const TASKS = [
        {
          id: 1,
          title: "buy milk",
          isCompleted: true,
        },
        {
          id: 2,
          title: "clean house",
          isCompleted: false,
        },
    ];
    
    class App extends Component {
      static template = xml`
        <div class="task-list">
          <t t-foreach="tasks" t-as="task" t-key="task.id">
            <div class="task">
              <input type="checkbox"
                   t-att-checked="task.isCompleted"/>
              <span><t t-esc="task.title"/></span>
            </div>
          </t>
        </div>`;
        
      tasks = TASKS;
    }

## Style

    <div
      class="task"
      t-att-class="task.isCompleted ? 'done' : ''">

# Look into Source Code

addons/web/static/src/xml/base.xml

== v13 架構分成 left right 兩部份 ==

    <t t-name="ControlPanel">
        <div class="o_control_panel">
            <div>
                <ol class="breadcrumb" role="navigation"/>
                <div class="o_cp_searchview" role="search">
                    <t t-if="widget.withSearchBar" t-call="SearchView"/>
                </div>
            </div>
            <div>
                <div class="o_cp_left">
                    <div class="o_cp_buttons" role="toolbar" aria-label="Control panel toolbar"/>
                    <aside class="o_cp_sidebar"/>
                </div>
                <div class="o_cp_right">
                    <div class="btn-group o_search_options position-static" role="search"/>
                    <nav class="o_cp_pager" role="search" aria-label="Pager"/>
                    <nav class="btn-group o_cp_switch_buttons" role="toolbar" aria-label="View switcher"/>
                </div>
            </div>
        </div>
    </t>


== v14 架構先分 top bottom 再分 left right ==

    <t t-name="web.ControlPanel" owl="1">
        <div class="o_control_panel">
            <div class="o_cp_top">
                <div class="o_cp_top_left">
                    <ol t-if="props.withBreadcrumbs" class="breadcrumb" role="navigation">
                        <li t-foreach="props.breadcrumbs" t-as="bc" t-key="bc.controllerID"
                            class="breadcrumb-item"
                            t-att-class="{ o_back_button: bc_index === props.breadcrumbs.length - 1 }"
                            t-att-accesskey="bc_last and 'b'"
                            t-on-click.prevent="trigger('breadcrumb-clicked', { controllerID: bc.controllerID })"
                            >
                            <a t-if="bc.title" href="#" t-esc="bc.title"/>
                            <em t-else="" class="text-warning">Unnamed</em>
                        </li>
                        <li class="breadcrumb-item active">
                            <t t-if="props.title" t-esc="props.title"/>
                            <em t-else="" class="text-warning">Unnamed</em>
                        </li>
                    </ol>
                </div>
                <div class="o_cp_top_right">
                    <div class="o_cp_searchview"
                        role="search"
                        t-ref="searchView"
                        >
                        <div t-if="props.withSearchBar" class="o_searchview" role="search" aria-autocomplete="list" >
                            <i class="o_searchview_icon fa fa-search"
                                title="Search..."
                                role="img"
                                aria-label="Search..."
                            />
                            <SearchBar t-if="props.withSearchBar" fields="fields"/>
                        </div>
                    </div>
                </div>
            </div>
            <div class="o_cp_bottom">
                <div class="o_cp_bottom_left">
                    <div class="o_cp_buttons" role="toolbar" aria-label="Control panel buttons" t-ref="buttons">
                        <t t-slot="buttons"/>
                    </div>
                    <ActionMenus t-if="props.actionMenus and props.actionMenus.items"
                        t-props="props.actionMenus"
                    />
                </div>
                <div class="o_cp_bottom_right">
                    <div class="btn-group o_search_options position-static"
                        role="search"
                        t-ref="searchViewButtons"
                        >
                        <t t-if="props.withSearchBar">
                            <FilterMenu t-if="props.searchMenuTypes.includes('filter')"
                                class="o_filter_menu"
                                fields="fields"
                            />
                            <GroupByMenu t-if="props.searchMenuTypes.includes('groupBy')"
                                class="o_group_by_menu"
                                fields="fields"
                            />
                            <ComparisonMenu t-if="props.searchMenuTypes.includes('comparison') and model.get('filters', f => f.type === 'comparison').length"
                                class="o_comparison_menu"
                            />
                            <FavoriteMenu t-if="props.searchMenuTypes.includes('favorite')"
                                class="o_favorite_menu"
                            />
                        </t>
                    </div>
                    <div class="o_cp_pager" role="search" t-ref="pager">
                        <Pager t-if="props.pager and props.pager.limit" t-props="props.pager"/>
                    </div>
                    <nav t-if="props.views.length gt 1" class="btn-group o_cp_switch_buttons" role="toolbar" aria-label="View switcher">
                        <t t-foreach="props.views" t-as="view" t-key="view.type">
                            <t t-call="web.ViewSwitcherButton"/>
                        </t>
                    </nav>
                </div>
            </div>
        </div>
    </t>

== 差異比較 ==

https://youtu.be/IrcQf4hgjtw 過往稱為 Widget 的程式碼，在 OWL 架構裡會被稱為 Component，在持續的改版過程中，議題之一是 Asset Management 也就是載入 Template 的新舊方式要能共存，新舊的程式寫法慣例也不同。

OWL 只是框架，需要和一個能產生 HTML 的工具合作，它是用來取代原本的 Widget 系統，在 QWEB 中可以同時用舊有 Widget 元件，也可以用新的 OWL 元件，所以沒有混用的問題。

可以參考 AbstractFieldOwl 做法，考慮用 container 方式做，把 template 內容定義成一個 widget 再透過 OWL component 去操作這個 widget。

v14 改用 this.env.models 看來 RPC 的用法都改了。

owl="1"

它把 model 的資料放到 props 之中，然後在 template 中取用 props 使用 QWEB 做為 client side template 來產生頁面。所以和舊的一樣，使用 qweb 做為 client side template。只是把原先的 context 用 owl 的 props 取代。讓整個框架看起來比較現代化。

OWL 用 useStore hook 來做狀態管理的動作。當 state 改變時，所有的 components 都可以監聽關的 state 並重新更新 DOM 的內容。達成 "react"的動作。所以 OWL 並不會直接對資料庫的改變做反應，而是要變資料庫的改變觸發一些 actions，然後由 action 來改變 state，最後才導至 QWEB 模版重新產生 DOM 造成畫面更新。

在抓取data還是必需依賴qweb，這樣才能使用xml繼承文件系統，這部份應該是不會動了

https://alanhou.org/odoo-14-owl/
qweb好處就是可以繼承修改嘛

http://youtube.com/watch?v=dkj4s_akje0 CybroSys, Console debug
app.js

    const { Componet } = owl;
    const { xml } = owl.tags;
    const { whenReady } = owl.utils;
    const { useState } = owl.hooks;
    
    // OWL Components
    
https://medium.com/@alle.aldine/how-to-show-list-of-events-created-in-odoo-erp-shows-in-reactjs-website-52d847fa86e
https://medium.com/@alle.aldine/how-to-build-a-blog-with-gatsby-and-odoo-a54aa6921a1e

[Odoo Owl Framework](https://www.youtube.com/watch?v=dki4s_akje0): 07:20 使用 npm 來建立專案骨架 10:20 App.env 11:18 Sub Environment 31:00 Demo Incru

  App.env = {
    _t: myTranslateFunction,
    user: {},
    services: {
    },
  }
  
  class FormComponent extends Component {
    constructor(parent, props) {
      super(parent, props);
      useSubEnv({ mykey: someValue });
    }
  }

[Build Owl Project](https://www.youtube.com/watch?v=ZxEhlOoYmWw): Components Hooks

