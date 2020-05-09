<template>
  <div class="home">
    <header>
      <nav-menu></nav-menu>
    </header>
    <section>
      <vue-table-dynamic
        :params="params"
        @select="onSelect"
        @select-all="onSelectAll"
        @selection-change="onSelectionChange"
        @row-click="onRowClick"
        @cell-click="onCellClick"
        @download="onDownload"
        ref="table"
      ></vue-table-dynamic>
    </section>
    <vue-msg :timeout="2000" :top="100" :right="20" ref="vueMsg"></vue-msg>
  </div>
</template>

<script>
import NavMenu from "./NavMenu.vue";
import VueButton from "./VueButton.vue";
import VueMsg from "vue-msgs";
import { saveAs } from "file-saver";
import { table, getBorderCharacters } from "table";
import data from "../../../data/convertjson.json";
const cloneDeep = require("lodash.clonedeep");

const defaultTableParams = {
  data: [
    [" #", `Name`, `URN`, `Version`, `Type`, `Submitted`, `Title | Description`]
  ],
  header: "row",
  height: "",
  headerHeight: 30,
  rowHeight: "auto",
  border: true,
  stripe: true,
  showCheck: true,
  enableSearch: true,
  columnWidth: [{ column: 0, width: 50 }],
  sort: [0, 1],
  edit: {},
  highlight: {},
  pagination: true
};

for (let i = 0; i < data.length; i++) {
  defaultTableParams.data.push([
    data[i].id,
    data[i].Name,
    data[i].URN,
    data[i].Version,
    data[i].Type,
    data[i].Submitter,
    data[i].Description
  ]);
}

const tableHeaderTypes = ["", "row", "column"];

export default {
  name: "Home",
  data() {
    return {
      params: cloneDeep(defaultTableParams),
      scrollBarOpts: {
        scrollPanel: { scrollingX: false },
        bar: { background: "#DFDFDF", opacity: 0.8 }
      },
      widthIncrement: 1,
      heightIncrement: 1,
      rowHeightIncrement: 1
    };
  },
  methods: {
    addRow() {
      let rowNum = this.params.data.length;
      let columnNum = this.params.data[0].length;

      if (rowNum >= 200) {
        return this.showMsg(
          "warning",
          "The number of rows cannot be more than 200."
        );
      }

      let newRow = [rowNum];
      for (let i = 1; i < columnNum; i++) {
        newRow.push(`${random()}-Cell`);
      }

      this.params.data.push(newRow);
    },
    deleteRow() {
      let rowNum = this.params.data.length;

      if (rowNum <= 1) {
        return this.showMsg(
          "warning",
          "The number of rows cannot be less than 1."
        );
      }

      this.params.data.pop();
    },
    addColumn() {
      let rowNum = this.params.data.length;
      let columnNum = this.params.data[0].length;

      if (columnNum >= 12) {
        return this.showMsg(
          "warning",
          "The number of columns cannot be more than 12."
        );
      }

      this.params.data[0].push(`Data${columnNum}`);
      for (let i = 1; i < rowNum; i++) {
        this.params.data[i].push(`${random()}-Cell`);
      }
    },
    deleteColumn() {
      let rowNum = this.params.data.length;
      let columnNum = this.params.data[0].length;

      if (columnNum <= 1) {
        return this.showMsg(
          "warning",
          "The number of columns cannot be less than 1."
        );
      }

      for (let i = 0; i < rowNum; i++) {
        this.params.data[i].pop();
      }
    },
    toggleHeader() {
      let curr = tableHeaderTypes.indexOf(this.params.header);
      if (curr < 0 || curr === tableHeaderTypes.length - 1)
        return (this.params.header = tableHeaderTypes[0]);

      this.params.header = tableHeaderTypes[curr + 1];
    },
    fixedHeader() {
      if (this.params.height) {
        this.params.height = "";
      } else {
        this.params.height = 170;
      }
    },
    toggleBorder() {
      this.params.border = !this.params.border;
    },
    toggleStripe() {
      this.params.stripe = !this.params.stripe;
    },
    toggleHighlight() {
      if (Object.keys(this.params.highlight).length > 0) {
        this.params.highlight = {};
      } else {
        this.params.highlight = { column: [-1] };
      }
    },
    toggleSelect() {
      this.params.showCheck = !this.params.showCheck;
    },
    toggleSearch() {
      this.params.enableSearch = !this.params.enableSearch;
    },
    toggleFilter() {
      if (this.params.filter.length > 0) {
        this.params.filter = [];
      } else {
        this.params.filter = [
          {
            column: 0,
            content: [
              { text: "> 3", value: 3 },
              { text: "> 5", value: 5 },
              { text: "> 7", value: 7 }
            ],
            method: (value, tableCell) => {
              return tableCell.data > value;
            }
          },
          {
            column: 2,
            content: [
              { text: "1-Cell", value: "1-Cell" },
              { text: "2-Cell", value: "2-Cell" },
              { text: "3-Cell", value: "3-Cell" }
            ],
            method: (value, tableCell) => {
              return String(tableCell.data)
                .toLocaleLowerCase()
                .includes(String(value).toLocaleLowerCase());
            }
          }
        ];
      }
    },
    toggleSort() {
      if (this.params.sort.length > 0) {
        this.params.sort = [];
      } else {
        this.params.sort = [0, 1];
      }
    },
    toggleEdit() {
      if (Object.keys(this.params.edit).length > 0) {
        this.params.edit = {};
      } else {
        this.params.edit = {
          row: [0, 1],
          column: [1, 2],
          cell: [[3, 3]]
        };
      }
    },
    togglePagination() {
      this.params.pagination = !this.params.pagination;
    },
    toPage() {
      if (this.$refs && this.$refs.table) {
        let target = Math.floor(Math.random() * 5 + 1);
        this.$refs.table.toPage(target);
      }
    },
    changeColumnWidth() {
      if (this.params.columnWidth[0].width >= 200) {
        this.widthIncrement = -1;
      } else if (this.params.columnWidth[0].width <= 50) {
        this.widthIncrement = 1;
      }
      this.params.columnWidth[0].width += 10 * this.widthIncrement;
    },
    changeHeaderHeight() {
      if (this.params.headerHeight >= 80) {
        this.heightIncrement = -1;
      } else if (this.params.headerHeight <= 30) {
        this.heightIncrement = 1;
      }
      this.params.headerHeight += 5 * this.heightIncrement;
    },
    changeRowHeight() {
      if (this.params.rowHeight >= 80) {
        this.rowHeightIncrement = -1;
      } else if (this.params.rowHeight <= 30) {
        this.rowHeightIncrement = 1;
      }
      this.params.rowHeight += 5 * this.rowHeightIncrement;
    },
    reset() {
      this.params = cloneDeep(defaultTableParams);
    },
    onSelect(checked, index, data) {
      console.log("onSelect: ", checked, index, data);
    },
    onSelectAll(isCheckedAll) {
      console.log("onSelectAll: ", isCheckedAll);
    },
    onSelectionChange(checkedDatas, checkedIndexs, checkedNum) {
      console.log(
        "onSelectionChange: ",
        checkedDatas,
        checkedIndexs,
        checkedNum
      );
    },
    onRowClick(index, data) {
      console.log("[ onRowClick ] : ", index, data);
    },
    onCellClick(rowIndex, columnIndex, data) {
      console.log("[ onCellClick ]: ", rowIndex, columnIndex, data);
    },
    onDownload(datas) {
      if (!(datas && datas.length > 0)) {
        return this.showMsg("warning", "The data is empty.");
      }

      let output = table(datas, {
        border: getBorderCharacters(`void`),
        columnDefault: {
          paddingLeft: 0,
          paddingRight: 2
        },
        drawHorizontalLine: () => {
          return false;
        }
      });

      let blob = new Blob([output], { type: "application/octet-stream" });
      saveAs(blob, "table");
    },
    // 消息弹框 type：success/info/warning/error
    showMsg(type, info) {
      if (
        this.$refs &&
        this.$refs.vueMsg &&
        typeof this.$refs.vueMsg.showMsg === "function"
      ) {
        this.$refs.vueMsg.showMsg(type, info);
      }
    }
  },
  components: { NavMenu, VueButton, VueMsg }
};
</script>

<style lang="scss" scoped>
.home {
  height: 100%;
  width: 100%;
  position: relative;
  header {
    width: 100%;
    height: 70px;
  }
  section {
    position: absolute;
    top: 5em;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 20px 25px;
  }
  .downloader {
    height: 0;
    width: 0;
    visibility: hidden;
  }
}
</style>
<style>
.v-show-border {
  border: 1px solid #ccc;
}
</style>
