---
title: Transfer Grid rows
page_title: Transfer Grid rows
description: Move a row from one grid to another using Kendo UI Sortable widget
---

# Transfer Grid rows

The following runnable sample demonstrates how to transfer Kendo UI Grid rows via the Kendo UI Sortable widget. The user can drag rows from the first grid to the second and vice versa. Reordering of
rows within the same grid is also implemented.

#### Example:

```html
<div id="grid1" style="width: 400px; float:left"></div>
<div id="grid2" style="width: 400px; float:left"></div>
<script src="http://demos.telerik.com/kendo-ui/content/shared/js/products.js"></script>
<script>
  $("#grid1").kendoGrid({
    dataSource: {
      data: products,
      schema: {
        model: {
          fields: {
            ProductName: { type: "string" },
            UnitPrice: { type: "number" },
            UnitsInStock: { type: "number" },
            Discontinued: { type: "boolean" }
          }
        }
      },
      pageSize: 5
    },
    columns: [
      "ProductName",
      { field: "UnitPrice", title: "Unit Price", format: "{0:c}", width: "130px" }
    ],
    dataBound: insertNoRecordsRow, //required to handle transfer row to empty grid scenario
    pageable: true
  });

  $("#grid2").kendoGrid({
    dataSource: {
      data: [],
      schema: {
        model: {
          fields: {
            ProductName: { type: "string" },
            UnitPrice: { type: "number" },
            UnitsInStock: { type: "number" },
            Discontinued: { type: "boolean" }
          }
        }
      },
      pageSize: 5
    },
    dataBound: insertNoRecordsRow, //required to handle transfer row to empty grid scenario
    pageable: true,
    columns: [
      "ProductName",
      { field: "UnitPrice", title: "Unit Price", format: "{0:c}", width: "130px" }
    ]
  });

  var dataItem = null;

  $(".k-grid table").kendoSortable({
    connectWith: '.k-grid table',
    filter: ">tbody >tr",
    disabled: ".no-drag", //do not allow transferring the no records row
    hint: $.noop,
    cursor: "move",
    placeholder: function(element) {
      return element.clone().addClass("k-state-hover").css("opacity", 0.65);
    },
    change: function(e) { //change event handler implementation may differ according to the scenario
      var grid = this.element.closest(".k-grid").data("kendoGrid");
      var skip = grid.dataSource.skip();
      var oldIndex = e.oldIndex + skip;
      var newIndex = e.newIndex + skip;

      if (e.action == "remove") {
        dataItem = grid.dataSource.getByUid(e.item.data("uid"));
        grid.dataSource.remove(dataItem);
      } else if (e.action == "receive" && dataItem != null) {
        grid.dataSource.insert(newIndex, dataItem);
        dataItem = null;
      } else if (e.action == "sort") {
        dataItem = grid.dataSource.getByUid(e.item.data("uid"));

        grid.dataSource.remove(dataItem);
        grid.dataSource.insert(newIndex, dataItem);
      }

      grid.saveChanges();
    }
  });

  function insertNoRecordsRow() {
    if (!this.dataSource.data().length) {
      this.tbody.append($("<tr class='no-drag' colspan='2'><td>No records</td></tr>")); 
    }
  }
</script>
```
