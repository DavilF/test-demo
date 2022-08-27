<template>
  <div class="moduleContainer">
    <div class="content">
      <div style="height:30px; margin-bottom:10px">
        <input type="text" v-model="searchValue" />
        <button @click="initPageData" style="margin-left: 20px">
          初始化文本
        </button>
        <button @click="handleExtract" style="margin-left: 20px">
          智能提取
        </button>
      </div>
      <div class="noData" v-if="!initContext">暂无数据</div>
      <div v-html="contextHtml" v-else></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LeftFrame",
  data() {
    return {
      searchValue: "",
      contextHtml: "",
      initContext: "",
    };
  },
  mounted() {
    //this.initPageData();
  },
  watch: {
    searchValue(val) {
      val = val.trim();
      this.contextHtml = this.originHtmlTextForSearch;
      if (val) {
        var reg = new RegExp(val, "gi");
        this.contextHtml = this.contextHtml.replace(reg, (res) => {
          return `<span class="highlight">${res}</span>`;
        });
      }
    },
  },
  methods: {
    initPageData() {
      this.initContext = `对于“插入”选项卡上的库，在设计时都充分考虑了其中的项与文档整体外观的协调性。 您可以使用这些库来插入表格、页眉、页脚、列表、封面以及其他文档构建基块。 您创建的图片、图表或关系图也将与当前的文档外观协调一致。
在“主页”选项卡上，通过从快速样式库中为所选文本选择一种外观，您可以方便地更改文档中所选文本的格式。 您还可以使用“主页”选项卡上的其他控件来直接设置文本格式。大多数控件都允许您选择是使用当前主题外观，还是使用某种直接指定的格式。
若要更改文档的整体外观，请在“页面布局”选项卡上选择新的“主题”元素。若要更改快速样式库中的可用外观，请使用“更改当前快速样式集”命令。主题库和快速样式库都提供了重置命令，因而您总是能够将文档外观还原为当前模板所包含的原始外观。
对于“插入”选项卡上的库，在设计时都充分考虑了其中的项与文档整体外观的协调性。 您可以使用这些库来插入表格、页眉、页脚、列表、封面以及其他文档构建基块。 您创建的图片、图表或关系图也将与当前的文档外观协调一致。
在“主页”选项卡上，通过从快速样式库中为所选文本选择一种外观，您可以方便地更改文档中所选文本的格式。 您还可以使用“主页”选项卡上的其他控件来直接设置文本格式。大多数控件都允许您选择是使用当前主题外观，还是使用某种直接指定的格式。
若要更改文档的整体外观，请在“页面布局”选项卡上选择新的“主题”元素。若要更改快速样式库中的可用外观，请使用“更改当前快速样式集”命令。主题库和快速样式库都提供了重置命令，因而您总是能够将文档外观还原为当前模板所包含的原始外观。
对于“插入”选项卡上的库，在设计时都充分考虑了其中的项与文档整体外观的协调性。 您可以使用这些库来插入表格、页眉、页脚、列表、封面以及其他文档构建基块。 您创建的图片、图表或关系图也将与当前的文档外观协调一致。
在“主页”选项卡上，通过从快速样式库中为所选文本选择一种外观，您可以方便地更改文档中所选文本的格式。 您还可以使用“主页”选项卡上的其他控件来直接设置文本格式。大多数控件都允许您选择是使用当前主题外观，还是使用某种直接指定的格式。
若要更改文档的整体外观，请在“页面布局”选项卡上选择新的“主题”元素。若要更改快速样式库中的可用外观，请使用“更改当前快速样式集”命令。主题库和快速样式库都提供了重置命令，因而您总是能够将文档外观还原为当前模板所包含的原始外观。
对于“插入”选项卡上的库，在设计时都充分考虑了其中的项与文档整体外观的协调性。 您可以使用这些库来插入表格、页眉、页脚、列表、封面以及其他文档构建基块。 您创建的图片、图表或关系图也将与当前的文档外观协调一致。
`;
      this.originHtmlTextForSearch = this.contextHtml = this.initContext;
    },

    handleExtract() {
      var extractArr = ["格式", "关系图"];
      var reg = new RegExp(extractArr.join("|"), "gi");
      this.contextHtml = this.initContext.replace(reg, (res) => {
        return `<span class="extractMark">${res}</span>`;
      });

      //存储值
      this.originHtmlTextForSearch = this.contextHtml;
    },
  },
};
</script>

<style scoped lang="scss">
.content {
  .noData {
    font-size: 30px;
    color: #ccc;
    margin: 100px;
  }
  ::v-deep {
    .highlight {
      background: orange;
    }
    .extractMark {
      box-sizing: border-box;
      border: solid 1px blue;
      background: lightblue;
    }
  }
}
</style>
