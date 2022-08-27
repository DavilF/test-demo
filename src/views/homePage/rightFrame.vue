<template>
  <div class="moduleContainer">
    <div v-for="(item, index) in list" :key="index" class="blockBox">
      <div class="hd">{{ item.title }}</div>
      <div class="bd">
        <div
          :class="['innerBox', { active: item.active }]"
          @dragover="handleDragover($event, item)"
          @dragleave="handleDragLeave($event, item)"
          @drop="handleDragDrop($event, item)"
        >
          <span class="placeholder" v-if="!item.tag.length">拖放安置区！</span>
          <ul class="list" v-else>
            <li v-for="(tagiItem, tagIndex) in item.tag" :key="tagIndex">
              {{ tagiItem.label }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "RightFrame",
  data() {
    return {
      list: [
        {
          title: "标题1",
          active: false,
          tag: [],
        },
        {
          title: "标题2",
          active: false,
          tag: [],
        },
        {
          title: "标题3",
          active: false,
          tag: [],
        },
      ],
    };
  },
  methods: {
    handleDragover(e, item) {
      e.preventDefault();
      clearTimeout(this.timer);
      item.active = true;
      //console.log("Dragover");
    },
    handleDragLeave(e, item) {
      var handler = () => {
        item.active = false;
        //console.log("DragLeave");
      };
      clearTimeout(this.timer);
      this.timer = setTimeout(handler, 100);
    },
    handleDragDrop(e, item) {
      item.active = false;
      var selectedText = window.getSelection().toString();
      //console.log(`选中的文本是:${selectedText}`);
      item.tag.push({
        label: selectedText,
      });
    },
  },
};
</script>

<style scoped lang="scss">
.moduleContainer {
  .blockBox {
    margin-bottom: 30px;
    .hd {
      font-size: 20px;
      font-weight: bold;
      margin-bottom: 10px;
    }
    .bd {
      .innerBox {
        padding: 10px;
        min-height: 100px;
        box-sizing: border-box;
        border: dashed 2px transparent;
        &.active {
          border-color: green;
          background: lightgreen;
        }
        .placeholder {
          color: #999;
        }

        .list {
          display: flex;
          flex-flow: wrap;
          box-sizing: border-box;
          li {
            box-sizing: border-box;
            list-style: none;
            padding: 0 10px;
            border: solid 1px #ccc;
            border-radius: 3px;
            margin: 10px;
            background: #efefef;
          }
        }
      }
    }
  }
}
</style>
