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

owl="1"

它把 model 的資料放到 props 之中，然後在 template 中取用 props 使用 QWEB 做為 client side template 來產生頁面。所以和舊的一樣，使用 qweb 做為 client side template。只是把原先的 context 用 owl 的 props 取代。讓整個框架看起來比較現代化。

